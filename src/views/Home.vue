<template>
  <div>
    <el-row :gutter="10" style="margin-top: 20px;margin-bottom: 40px">
      <el-col :span="6">
        <el-card style="color: #409EFF">
          <div><i class="el-icon-user-solid" /> 用户总数</div>
          <div  style="padding:10px 0; text-align: center ; font-weight: bold">
            {{ homeEcharts.userCount }}
          </div>
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card style="color: #E6A23C">
          <div><i class="el-icon-picture" /> 图片总数</div>
          <div style="padding:10px 0; text-align: center ; font-weight: bold">
            {{ homeEcharts.pictureCount }}
          </div>
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card style="color: #67C23A">
          <div><i class="el-icon-collection-tag" /> 标签总数</div>
          <div style="padding:10px 0; text-align: center ; font-weight: bold">
            {{ homeEcharts.tagCount }}
          </div>
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card style="color: #F56C6C">
          <div><i class="el-icon-warning-outline" /> 禁用总数</div>
          <div style="padding:10px 0; text-align: center ; font-weight: bold">
            {{ homeEcharts.enableCount }}
          </div>
        </el-card>
      </el-col>
    </el-row>
      <el-card style="margin: 10px 0">
        <div style="padding-bottom: 20px; font-size: 24px">富 文 本 系 统 公 告</div>
        <el-collapse accordion v-for="(item, index) in noticeRich" >
          <el-collapse-item :name="index + ''">
            <template slot="title">
              <span style="font-size: 20px; color: #E6A23C">{{ item.name }}</span><i style="color: #E6A23C" class="header-icon el-icon-info"></i>
              <span style="margin-left: 20px">{{ item.time }}</span>
            </template>
            <div>
              <div style="padding: 10px 0"><el-image :src="item.img"></el-image></div>
              <div v-html="item.content"></div>
            </div>
          </el-collapse-item>
        </el-collapse>
      </el-card>
    </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      homeEcharts :{
          userCount : 0,
          pictureCount : 0,
          tagCount : 0,
          enableCount : 0
      },
      selectTagData :{},
      activeNames: ['0'],
      user: localStorage.getItem("user") ? JSON.parse(localStorage.getItem("user")) : {},
      notice: [],
      noticeRich: []
    }
  },
  mounted() { //页面元素渲染之后再触发
    this.request.get("/echarts/homeCount").then(res => {
      this.homeEcharts.userCount = res.data.userCount
      this.homeEcharts.pictureCount = res.data.pictureCount
      this.homeEcharts.tagCount = res.data.tagCount
      this.homeEcharts.enableCount = res.data.enableCount
    })
  },
  created() {
    this.request.get("/notice/type/2").then(res => {
      this.noticeRich = res.data.splice(0, 5)
    })
  }
}
</script>

<style scoped>

</style>
