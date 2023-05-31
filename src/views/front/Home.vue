<template>
  <div>
    <div style="margin: 10px 0;" >
      <el-carousel :interval="8000" type="card" height="150px" style="margin-top: 20px">
        <el-carousel-item v-for="item in carousel" >
          <img :src="item" alt="" style="width: 100%">
        </el-carousel-item>
      </el-carousel>
    </div>


    <div><h3>推荐作品</h3></div>
    <div style="margin: 10px 0">
      <el-row :gutter="10">
        <el-col :span="4" v-for="item in pics" :key="item.id" style="margin-bottom: 10px">
          <div style="border:1px solid #ffffff; ">
            <img @click="$router.push('/front/picDetail?id=' + item.id)" :src="item.img" alt="" style="cursor: pointer;width: 100%; border-radius: 10px; object-fit: cover" height="200px" >
            <div style="color: #666; padding: 1px; margin-left: 10px; margin-right: 10px" >
              <b ># {{ item.name }}</b>
              <el-button icon="el-icon-star-off" circle style="float: right"></el-button>
            </div>
          </div>
          <div style="color: #666; padding: 1px; margin-left: 10px; margin-right: 10px" >投稿人：{{ item.user }}</div>
        </el-col>
      </el-row>
    </div>

    <div><h3>全部作品</h3></div>
    <div style="margin: 10px 0">
      <el-row :gutter="10">
        <el-col :span="4" v-for="item in picS" :key="item.id" style="margin-bottom: 10px">
          <div style="border:1px solid #ffffff; ">
            <img @click="$router.push('/front/picDetail?id=' + item.id)" :src="item.img" alt="" style="cursor: pointer;width: 100%; border-radius: 10px; object-fit: cover" height="200px" >
            <div style="color: #666; padding: 1px; margin-left: 10px; margin-right: 10px" >
              <b ># {{ item.name }}</b>
              <el-button icon="el-icon-star-off" circle style="float: right"></el-button>
            </div>
          </div>
          <div style="color: #666; padding: 1px; margin-left: 10px; margin-right: 10px" >投稿人：{{ item.user }}</div>
        </el-col>
      </el-row>
    </div>

    <!--  回到顶部  -->
    <ul class="tops" @click="goTop">
      <li class="top1">
        <button class="top2">
          <svg viewBox="0 0 120 120" class="top3">
            <polyline points="60,105 60,8"></polyline>
            <polyline points="10,57 60,8 110,57"></polyline>
          </svg>
        </button>
      </li>
    </ul>

  </div>
</template>

<script>
export default {
  name: "FrontHome",
  data() {
    return {
      carousel: [
        'http://localhost:9090/file/7f9662cf9e95491f925f38e8fc59e4e4.jpg',
        'http://localhost:9090/file/201a82c8a7d44b69b20e4ee3528f595e.jpg',
        'http://localhost:9090/file/532ea4095f0c4417a7cd73858b330085.jpg',
      ],
      pics: [],
      picS: []
    }
  },
  created() {
    this.load()
  },
  methods: {
    load() {
      this.request.get("/echarts/file/front/rand").then(res => {
        this.pics = res.data
        this.pics = res.data.splice(0, 12)
      })

      this.request.get("/echarts/file/front/all").then(res => {
        this.picS = res.data
      })
    },
    goTop() {
      let top = document.documentElement.scrollTop || document.body.scrollTop
      // 实现滚动效果
      const timeTop = setInterval(() => {
        document.body.scrollTop = document.documentElement.scrollTop = top -= 50
        if (top <= 0) {
          clearInterval(timeTop)
        }
      }, 0)
    }
  }
}
</script>

<style>
.tops {
  position: fixed;
  z-index: 1;
  right: 28px;
  bottom: 34px;
  margin: -5px 0px;
  padding: 0px;
}
.top1 {
   margin: 5px 0px;
   padding: 0px;
   list-style: none;
 }
.top2 {
  display: inline-block;
  box-sizing: border-box;
  width: 48px;
  height: 48px;
  border-radius: 24px;
  padding: 12px;
  border: none;
  cursor: pointer;
  color: rgb(255, 255, 255);
  background-color: rgba(0, 0, 0, 0.32);
  transition: opacity 0.3s ease 0s;
}
.top3 {
  width: 24px;
  height: 24px;
  stroke: currentcolor;
  fill: none;
  stroke-width: 10;
  stroke-linecap: round;
  stroke-linejoin: round;
}
</style>
