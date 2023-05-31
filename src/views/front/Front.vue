<template>
  <div>
    <!--    头部-->
    <div style="display: flex; height: 60px; line-height: 60px;">
      <div style="width: 300px; display: flex; padding-left: 30px">
        <div style="width: 60px">
          <div style="width: 80px; position: relative; top: 10px; right: 0">
            <h1>icuH</h1>
          </div>
        </div>
      </div>
      <div style="flex: 1" >
        <el-menu :default-active="'1'" class="el-menu-demo" mode="horizontal" router>
          <el-menu-item index="/front/home">首页</el-menu-item>
          <el-menu-item index="/front/article">文章列表</el-menu-item>
<!--          <el-input :disabled="true" prefix-icon="el-icon-search" placeholder="尝试着输入点什么..." v-model="input"
                    clearable style="margin-left:210px;width:25%; height: 50px;">
          </el-input>-->
        </el-menu>
      </div>
      <div style="width: 200px">
        <div v-if="!user.username" style="text-align: right; padding-right: 30px">
          <el-button @click="$router.push('/login')">登录</el-button>
          <el-button @click="$router.push('/register')">注册</el-button>
        </div>
        <div v-else>
          <el-dropdown style="width: 180px; cursor: pointer; text-align: right">
            <div style="display: inline-block">
              <img :src="user.avatarUrl" alt=""
                   style="width: 30px; border-radius: 50%; position: relative; top: 10px; right: 5px">
              <i class="el-icon-arrow-down" style="margin-left: 3px"></i>
            </div>
            <el-dropdown-menu slot="dropdown" style="width: 100px; margin-right: 70px; text-align: center">
              <el-dropdown-item style="font-size: 14px; padding: 5px 0">
                <span style="text-decoration: none" @click="$router.push('/password')">修改密码</span>
              </el-dropdown-item>
              <el-dropdown-item style="font-size: 14px; padding: 5px 0">
                <span style="text-decoration: none" @click="$router.push('/person')">个人信息</span>
              </el-dropdown-item>
              <el-dropdown-item style="font-size: 14px; padding: 5px 0">
                <span style="text-decoration: none" @click="logout">退出</span>
              </el-dropdown-item>
            </el-dropdown-menu>
            <el-button type="primary" style="margin-left: 5px; border-radius: 15px">
              <b style="font-size: 13px" @click="$router.push('/home')">投稿</b><i class="el-icon-upload el-icon--right"></i>
            </el-button>
          </el-dropdown>
        </div>
      </div>
    </div>

    <!--  动态标签  -->
    <div style="margin-left: 250px; margin-top: 15px">
      <div class=" tags" >
        <a class="tag1" v-for="(item,a) in tags" :key="item.id"  style="cursor: pointer;margin-left: 10px;" :class="tagBg[a]">
          <div  @click="$router.replace('/front/tagDetail?id=' + item.id)">
            #{{ item.name }}
          </div>
        </a>
      </div>
    </div>

    <div style="width: 1250px; margin: 0 auto">
      <router-view />
    </div>
  </div>
</template>

<script>
import {resetRouter} from "@/router";

export default {
  name: "Front",
  data() {
    return {
      input: '',
      tags:[],
      tagBg: ["tagBg1","tagBg2","tagBg3","tagBg4","tagBg5"],
      user: localStorage.getItem("user") ? JSON.parse(localStorage.getItem("user")) : {}
    }
  },
  created() {
    this.load()
  },
  methods: {
    load() {
      this.request.get("/tag/").then(res => {
        this.tags = res.data
      })
    },
    logout() {
      this.$router.push("/front/home")
      localStorage.removeItem("user")
      resetRouter()
      this.$message.success("退出成功")
      this.$router.go(0)
    }
  }
}
</script>

<style>
.tags {
  display: flex;
}
.tag1 {
  box-sizing: border-box;
  text-decoration: none;
  display: flex;
  -webkit-box-align: center;
  align-items: center;
  border-radius: 4px;
  height: 40px;
  padding-right: 24px;
  padding-left: 24px;
  color: rgb(255, 255, 255);
}
.tagBg1 {
  background-color: #869fff;
}
.tagBg2 {
  background-color: #ff86e3;
}
.tagBg3 {
  background-color: #86ff8c;
}
.tagBg4 {
  background-color: #ffeb86;
}
.tagBg5 {
  background-color: #ff8698;
}

</style>
