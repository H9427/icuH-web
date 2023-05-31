<template>
  <div>
    <div style="margin: 10px 0">
      <el-input style="width: 200px" placeholder="请输入名称" suffix-icon="el-icon-search" v-model="name"></el-input>
      <el-input style="width: 200px" placeholder="请输入标签" suffix-icon="el-icon-collection-tag"  class="ml-5" v-model="tag"></el-input>
      <el-button class="ml-5" type="primary" @click="load">搜索</el-button>
      <el-button type="warning" @click="reset">重置</el-button>
    </div>
    <div style="margin: 10px 0">
      <el-button type="primary" @click="handleAdd">上传插画 <i class="el-icon-circle-plus-outline"></i></el-button>
      <el-popconfirm
          class="ml-5"
          confirm-button-text='确定'
          cancel-button-text='我再想想'
          icon="el-icon-info"
          icon-color="red"
          title="您确定批量删除这些数据吗？"
          @confirm="delBatch"
      >
        <el-button type="danger" slot="reference" v-if="user.role === 'ROLE_ADMIN'">批量删除 <i class="el-icon-remove-outline"></i></el-button>
      </el-popconfirm>
    </div>

    <el-table :data="tableData" border stripe :header-cell-class-name="'headerBg'"  @selection-change="handleSelectionChange">
      <el-table-column type="selection" width="55"></el-table-column>
      <el-table-column prop="id" label="ID" width="80" sortable></el-table-column>
      <el-table-column prop="name" label="插画名称" width="80"></el-table-column>
      <el-table-column prop="tag" label="插画标签" width="80">
        <template slot-scope="scope">
          <el-tag type="primary" v-if="scope.row.tag === 1">二次元</el-tag>
          <el-tag type="success" v-if="scope.row.tag === 2">风景</el-tag>
          <el-tag type="info" v-if="scope.row.tag === 3">汽车</el-tag>
          <el-tag type="warning" v-if="scope.row.tag === 4">美食</el-tag>
          <el-tag type="danger" v-if="scope.row.tag === 5">人像</el-tag>
        </template>
      </el-table-column>
      <el-table-column prop="user" label="上传者" width="80"></el-table-column>
      <el-table-column prop="description" label="插画描述" width="150"></el-table-column>
      <el-table-column label="插画" width="121"><template slot-scope="scope"><el-image style="width: 100px; height: 100px" :src="scope.row.img" :preview-src-list="[scope.row.img]"></el-image></template></el-table-column>
      <el-table-column prop="likes" label="点赞数" width="60"></el-table-column>
      <el-table-column prop="loves" label="爱心数" width="60"></el-table-column>
      <el-table-column prop="time" label="上传时间" width="120"></el-table-column>
      <el-table-column label="启用" width="100">
        <template slot-scope="scope">
          <el-switch v-model="scope.row.enable" active-color="#13ce66" inactive-color="#ccc" @change="changeEnable(scope.row)"></el-switch>
        </template>
      </el-table-column>
      <el-table-column prop="state" label="插画状态" width="120"></el-table-column>
      <el-table-column label="审核" width="210">
        <template v-slot="scope">
          <el-button type="success" @click="changeState(scope.row, '审核通过')" :disabled="scope.row.state !== '待审核'">审核通过</el-button>
          <el-button type="danger" @click="changeState(scope.row, '审核不通过')" :disabled="scope.row.state !== '待审核'">审核不通过</el-button>
        </template>
      </el-table-column>
      <el-table-column prop="remark" label="禁用描述" ></el-table-column>
      <el-table-column label="操作"  width="180" align="center">
        <template slot-scope="scope" >
          <el-button type="success" @click="handleEdit(scope.row)">编辑 <i class="el-icon-edit"></i></el-button>
          <el-popconfirm
              class="ml-5"
              confirm-button-text='确定'
              cancel-button-text='我再想想'
              icon="el-icon-info"
              icon-color="red"
              title="您确定删除吗？"
              @confirm="del(scope.row.id)"
          >
            <el-button type="danger" slot="reference">删除 <i class="el-icon-remove-outline"></i></el-button>
          </el-popconfirm>
        </template>
      </el-table-column>
    </el-table>
    <div style="padding: 10px 0">
      <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page="pageNum"
          :page-sizes="[2, 5, 10, 20]"
          :page-size="pageSize"
          layout="total, sizes, prev, pager, next, jumper"
          :total="total">
      </el-pagination>
    </div>

    <el-dialog title="插画信息" :visible.sync="dialogFormVisible" width="30%" :close-on-click-modal="false">
      <el-form label-width="100px" size="small" style="width: 90%">
        <el-form-item label="插画名称">
          <el-input v-model="form.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="插画标签">
          <el-input v-model="form.tag" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="插画描述">
          <el-input v-model="form.description" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="插画链接">
          <el-upload action="http://localhost:9090/file/upload" ref="img" :on-success="handleImgUploadSuccess">
            <el-button size="small" type="primary">点击上传</el-button>
          </el-upload>
        </el-form-item>
<!--        <el-form-item label="点赞数">
          <el-input v-model="form.likes" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="爱心数">
          <el-input v-model="form.loves" autocomplete="off"></el-input>
        </el-form-item>-->
        <el-form-item label="禁用描述">
          <el-input v-model="form.remark" autocomplete="off" type="textarea"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="save">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: "Pic",
  data() {
    return {
      tableData: [],
      total: 0,
      pageNum: 1,
      pageSize: 10,
      name: "",
      tag: "",
      form: {},
      dialogFormVisible: false,
      multipleSelection: [],
      user: localStorage.getItem("user") ? JSON.parse(localStorage.getItem("user")) : {}
    }
  },
  created() {
    this.load()
  },
  methods: {
    changeState(row, state) {
      /*stringify：把对象变成字符串*/
      this.form = JSON.parse(JSON.stringify(row))
      this.form.state = state;
      this.save();
    },
    load() {
      this.request.get("/pic/page", {
        params: {
          pageNum: this.pageNum,
          pageSize: this.pageSize,
          name: this.name,
          tag: this.tag
        }
      }).then(res => {
        this.tableData = res.data.records
        this.total = res.data.total
      })
    },
    save() {
      this.request.post("/pic", this.form).then(res => {
        if (res.code === '200') {
          this.$message.success("保存成功")
          this.dialogFormVisible = false
          this.load()
        } else {
          this.$message.error("保存失败")
        }
      })
    },
    handleAdd() {
      this.dialogFormVisible = true
      this.form = {}
      this.$nextTick(() => {
        if(this.$refs.img) {
          this.$refs.img.clearFiles();
        }
        if(this.$refs.file) {
          this.$refs.file.clearFiles();
        }
      })
    },
    handleEdit(row) {
      this.form = JSON.parse(JSON.stringify(row))
      this.dialogFormVisible = true
      this.$nextTick(() => {
        if(this.$refs.img) {
          this.$refs.img.clearFiles();
        }
        if(this.$refs.file) {
          this.$refs.file.clearFiles();
        }
      })
    },
    del(id) {
      this.request.delete("/pic/" + id).then(res => {
        if (res.code === '200') {
          this.$message.success("删除成功")
          this.load()
        } else {
          this.$message.error("删除失败")
        }
      })
    },
    handleSelectionChange(val) {
      console.log(val)
      this.multipleSelection = val
    },
    delBatch() {
      if (!this.multipleSelection.length) {
        this.$message.error("请选择需要删除的数据")
        return
      }
      let ids = this.multipleSelection.map(v => v.id)  // [{}, {}, {}] => [1,2,3]
      this.request.post("/pic/del/batch", ids).then(res => {
        if (res.code === '200') {
          this.$message.success("批量删除成功")
          this.load()
        } else {
          this.$message.error("批量删除失败")
        }
      })
    },
    reset() {
      this.name = ""
      this.tag = ""
      this.load()
    },
    handleSizeChange(pageSize) {
      console.log(pageSize)
      this.pageSize = pageSize
      this.load()
    },
    handleCurrentChange(pageNum) {
      console.log(pageNum)
      this.pageNum = pageNum
      this.load()
    },
    handleFileUploadSuccess(res) {
      this.form.file = res
    },
    handleImgUploadSuccess(res) {
      this.form.img = res
    },
    download(url) {
      window.open(url)
    },
    changeEnable(row) {
      this.request.post("/pic/update", row).then(res => {
        if (res.code === '200' ) {
          this.form = JSON.parse(JSON.stringify(row))
          if (this.form.state === '待审核') {
            this.$message.error("操作失败");
          } else {
            this.$message.success("操作成功");
          }
        }
      })
    },
  }
}
</script>


<style>
.headerBg {
  background: #eee!important;
}
</style>
