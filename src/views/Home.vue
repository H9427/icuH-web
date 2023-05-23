<template>
  <div>
    <div style="height: 60px; line-height: 60px; border-bottom: 1px sold #ccc; background-color: aliceblue">
      <!-- 头部 -->
      <div style="display: flex">
        <div style="width: 200px; color: dodgerblue; font-weight: bold; padding-left: 20px; font-size: 18px">icuH后台管理系统</div>
        <div style="flex: 1; display: flex">
          <div style="flex: 1">中间</div>
          <div style="width: 200px; text-align: right; padding-right: 10px">头像</div>
        </div>
      </div>
    </div>

    <div style="display: flex">
      <div style="width: 200px; min-height: calc(100vh - 60px); border-hight: 1px solid #ccc">
        <!-- 左侧导航栏 -->
        <el-menu default-active="2" class="el-menu-vertical-demo">
          <el-sub-menu index="1">
            <template #title>
              <el-icon><location /></el-icon>
              <span>Navigator One</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="1-1">item one</el-menu-item>
            </el-menu-item-group>
            <el-sub-menu index="1-4">
              <template #title>item four</template>
              <el-menu-item index="1-4-1">item one</el-menu-item>
            </el-sub-menu>
          </el-sub-menu>
          <el-menu-item index="2">
            <el-icon><icon-menu /></el-icon>
            <span>Navigator Two</span>
          </el-menu-item>
        </el-menu>
      </div>

      <!-- 主体部分 -->
      <div style="flex: 1; padding: 10px">
        <!-- 主体-搜索框 -->
        <div>
          <el-input v-model="name" placeholder="请输入名称" style="width: 200px; margin-left: 5px" :suffix-icon="User" />
          <el-input v-model="email" placeholder="请输入邮箱" style="width: 200px; margin-left: 5px" :suffix-icon="Message" />
          <el-input v-model="address" placeholder="请输入地址" style="width: 200px; margin-left: 5px" :suffix-icon="Position" />
          <button class="btn btn-info btn-sm" style="margin-left: 5px">
            <span>搜索&nbsp;</span>
            <el-icon><Search /></el-icon>
          </button>
          <button class="btn btn-warning btn-sm" style="margin-left: 5px">
            <span>重置&nbsp;</span>
            <el-icon><Refresh /></el-icon>
          </button>
          <el-button>123</el-button>
        </div>

        <div style="margin-top: 10px">
          <button class="btn btn-accent btn-sm" style="margin-left: 5px" @click="handleAdd">
            <span>新增&nbsp;</span>
            <el-icon><CirclePlus /></el-icon>
          </button>
          <button class="btn btn-error btn-sm" style="margin-left: 5px">
            <span>批量删除&nbsp;</span>
            <el-icon><Remove /></el-icon>
          </button>
        </div>

        <!-- 主体-表格内容 -->
        <div style="margin: 10px 0">
          <div class="overflow-x-auto w-full">
            <el-table :data="state.tableData" stripe border @selection-change="handleSelectionChange">
              <el-table-column type="selection" width="55" />
              <el-table-column prop="id" label="id" width="80"></el-table-column>
              <el-table-column prop="username" label="用户名" width="120"></el-table-column>
              <el-table-column prop="nickname" label="昵称" width="120"></el-table-column>
              <el-table-column prop="email" label="邮箱" width="150"></el-table-column>
              <el-table-column prop="address" label="地址" width="200"></el-table-column>
              <el-table-column prop="phone" label="电话" width="120"></el-table-column>
              <el-table-column prop="role" label="角色" width="120"></el-table-column>
              <el-table-column prop="create_time" label="创建时间" width="200"></el-table-column>
              <el-table-column label="操作" width="175px">
                <template #default="scope">
                  <button class="btn btn-accent btn-sm" @click="handleEdit(scope.row)">
                    <span>编辑&nbsp;</span>
                    <el-icon><Edit /></el-icon>
                  </button>
                  <button class="btn btn-error btn-sm" style="margin-left: 5px" @click="deleteRow(scope.row.id)">
                    <span>删除&nbsp;</span>
                    <el-icon><Delete /></el-icon>
                  </button>
                </template>
              </el-table-column>
            </el-table>
          </div>
        </div>

        <!-- 主体-分页部分 -->
        <div>
          <el-pagination v-model:current-page="pageNum" v-model:page-size="pageSize" small background layout="total, sizes, prev, pager, next ,jumper" :total="50" />
        </div>
      </div>
    </div>
  </div>

  <el-dialog v-model="dialogFormVisible" title="新增用户信息" width="23%">
    <el-form :model="state.form">
      <el-form-item label="用户名" prop="username" style="margin-left: 10px">
        <input type="text" placeholder="请输入用户名" class="input input-bordered input-sm w-full max-w-xs" v-model="state.form.username" autocomplete="off" />
      </el-form-item>
      <el-form-item v-if="!state.form.id" label="密码" prop="password" style="margin-left: 10px">
        <input style="margin-left: 13px" type="password" placeholder="请输入密码" class="input input-bordered input-sm w-full max-w-xs" v-model="state.form.password" autocomplete="off" />
      </el-form-item>
      <el-form-item label="昵称" style="margin-left: 10px">
        <input style="margin-left: 13px" type="text" placeholder="请输入昵称" class="input input-bordered input-sm w-full max-w-xs" v-model="state.form.nickname" autocomplete="off" />
      </el-form-item>
      <el-form-item label="邮箱" style="margin-left: 10px">
        <input style="margin-left: 13px" type="text" placeholder="请输入邮箱" class="input input-bordered input-sm w-full max-w-xs" v-model="state.form.email" autocomplete="off" />
      </el-form-item>
      <el-form-item label="地址" style="margin-left: 10px">
        <input style="margin-left: 13px" type="text" placeholder="请输入地址" class="input input-bordered input-sm w-full max-w-xs" v-model="state.form.address" autocomplete="off" />
      </el-form-item>
      <el-form-item label="电话" style="margin-left: 10px">
        <input style="margin-left: 13px" type="text" placeholder="请输入电话" class="input input-bordered input-sm w-full max-w-xs" v-model="state.form.phone" autocomplete="off" />
      </el-form-item>
      <el-form-item label="角色" style="margin-left: 10px">
        <input style="margin-left: 13px" type="text" placeholder="请选择角色" class="input input-bordered input-sm w-full max-w-xs" v-model="state.form.role" autocomplete="off" />
      </el-form-item>
    </el-form>

    <template #footer>
      <span class="dialog-footer">
        <button class="btn btn-outline btn-info btn-sm" @click="save" style="margin-left: 5px">
          <span>确定</span>
        </button>
        <button class="btn btn-outline btn-error btn-sm" @click="dialogFormVisible = false" style="margin-left: 5px">
          <span>取消</span>
        </button>
      </span>
    </template>
  </el-dialog>
</template>

<script setup>
import { reactive, ref } from "vue";
import request from "../request";
import { Document, Menu as IconMenu, Location, Setting, Search, Refresh, CirclePlus, User, Remove, Edit, Delete, Message, Position } from "@element-plus/icons-vue";
import { ElMessage } from "element-plus";
import Aside from "@/components/Front/Aside.vue";

const pageNum = ref(1);
const pageSize = ref(2);
const state = reactive({
  tableData: [],
  form: {},
});

const multipleSelection = ref([]);
const handleSelectionChange = (val) => {
  multipleSelection.value = val;
};

const load = () => {
  // 表格数据
  request.get("/user").then((res) => {
    state.tableData = res;
  });
};
load();

const dialogFormVisible = ref(false);
// 新增弹框
const handleAdd = () => {
  dialogFormVisible.value = true;
  state.form = {};
};

//编辑弹框
const handleEdit = (row) => {
  dialogFormVisible.value = true;
  state.form = JSON.parse(JSON.stringify(row));
};

// 新增
const save = () => {
  request
    .post("/user", state.form)
    .then((res) => {
      ElMessage.success("保存成功");
      dialogFormVisible.value = false;
      //刷新表格
      load();
    })
    .catch((error) => {
      ElMessage.error("保存失败：" + error.message);
      dialogFormVisible.value = false;
    });
};

const deleteRow = (id) => {
  request.delete("/user/" + id).then((res) => {
    if (res === 1) {
      ElMessage.success("删除成功");
    } else {
      ElMessage.success("删除失败");
    }
    load();
  });
};
</script>

<style scoped></style>
