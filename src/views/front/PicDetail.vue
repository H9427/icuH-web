<template>
  <div>
    <div style="margin-top: 35px">
      <h3># {{ pics.name }}</h3>
    </div>

    <div style="margin-top: 20px">
      <el-row style="display: flex; justify-content: space-between">
        <el-col :span="17" style="margin-right: 30px; height: 50%; display: flex; align-items: center">
          <el-card style="border-radius: 20px; width: 100%">
            <div style="display: flex; justify-content: center">
              <img :src="pics.img" style="max-width: 100%; max-height: 100%" />
            </div>
          </el-card>
        </el-col>

        <!-- 待完善 -->
        <!-- <el-col :span="7">
          <el-card>
            {{ pics.user }}
            {{ pics }}
          </el-card>
        </el-col> -->
      </el-row>
    </div>

    <div>
      <div>
        <a href="">
          <i class="el-icon-more" style="float: right; margin-top: 7px; margin-right: 25px; margin-left: 13px"></i>
        </a>
      </div>

      <!--   爱心   -->
      <div>
        <a href="">
          <svg viewBox="0 0 32 32" width="32" height="32" style="float: right; margin-left: 15px; margin-right: 5px">
            <defs>
              <mask id="uid-mask-1">
                <rect x="0" y="0" width="32" height="32" fill="white"></rect>
                <path d="M16,11.3317089 C15.0857201,9.28334665 13.0491506,7.5 11,7.5C8.23857625,7.5 6,9.73857647 6,12.5 C6,17.4386065 9.2519779,21.7268174 15.7559337,25.3646328C15.9076021,25.4494645 16.092439,25.4494644 16.2441073,25.3646326 C22.7480325,21.7268037 26,17.4385986 26,12.5C26,9.73857625 23.7614237,7.5 21,7.5 C18.9508494,7.5 16.9142799,9.28334665 16,11.3317089 Z" class="sc-j89e3c-0 dUurgf"></path>
              </mask>
            </defs>
            <g mask="url(#uid-mask-1)">
              <path d="M21,5.5 C24.8659932,5.5 28,8.63400675 28,12.5 C28,18.2694439 24.2975093,23.1517313 17.2206059,27.1100183C16.4622493,27.5342993 15.5379984,27.5343235 14.779626,27.110148 C7.70250208,23.1517462 4,18.2694529 4,12.5C4,8.63400691 7.13400681,5.5 11,5.5 C12.829814,5.5 14.6210123,6.4144028 16,7.8282366C17.3789877,6.4144028 19.170186,5.5 21,5.5 Z"></path>
              <path d="M16,11.3317089 C15.0857201,9.28334665 13.0491506,7.5 11,7.5C8.23857625,7.5 6,9.73857647 6,12.5 C6,17.4386065 9.2519779,21.7268174 15.7559337,25.3646328C15.9076021,25.4494645 16.092439,25.4494644 16.2441073,25.3646326 C22.7480325,21.7268037 26,17.4385986 26,12.5C26,9.73857625 23.7614237,7.5 21,7.5 C18.9508494,7.5 16.9142799,9.28334665 16,11.3317089 Z" class="sc-j89e3c-0 dUurgf"></path>
            </g>
          </svg>
        </a>
      </div>

      <div>
        <a href="">
          <b style="float: right; margin-top: 5px; margin-left: 2px; color: #000000">赞!</b>
          <!--  赞  -->
          <svg style="height: 13px; margin-top: 10px; float: right" class="_3eF4D7o" viewBox="0 0 12 12">
            <path
              d="M2,6 C0.8954305,6 0,5.1045695 0,4 C0,2.8954305 0.8954305,2 2,2 C3.1045695,2 4,2.8954305 4,4C4,5.1045695 3.1045695,6 2,6 Z M10,6 C8.8954305,6 8,5.1045695 8,4 C8,2.8954305 8.8954305,2 10,2C11.1045695,2 12,2.8954305 12,4 C12,5.1045695 11.1045695,6 10,6 Z M2.1109127,8.8890873C1.72038841,8.498563 1.72038841,7.86539803 2.1109127,7.47487373C2.501437,7.08434944 3.13460197,7.08434944 3.52512627,7.47487373
              C4.89196129,8.84170876 7.10803871,8.84170876 8.47487373,7.47487373
              C8.86539803,7.08434944 9.498563,7.08434944 9.8890873,7.47487373
              C10.2796116,7.86539803 10.2796116,8.498563 9.8890873,8.8890873
              C7.74120369,11.0369709 4.25879631,11.0369709 2.1109127,8.8890873 Z"></path>
          </svg>
        </a>
      </div>
    </div>

    <div style="margin-top: 20px; margin-left: 30px; color: #8c939d; font-size: 16px">
      {{ pics.description }}
    </div>

    <div style="margin-bottom: 20px">
      <div style="font-size: 14px; margin-left: 30px; margin-top: 10px">
        <i class="el-icon-user-solid" style="color: #8c939d"></i> <span style="color: #8c939d"> {{ pics.user }}</span> <i class="el-icon-time" style="margin-left: 10px; color: #8c939d"></i> <span style="color: #8c939d"> {{ pics.time }}</span>
      </div>
    </div>

    <div>
      <div style="margin: 10px 0">
        <div style="border-bottom: 1px solid orangered; padding: 10px 0; font-size: 20px">评论</div>
        <div style="padding: 10px 0">
          <el-input size="small" type="textarea" v-model="reviewForm.review"></el-input>
        </div>
        <div class="pd-10" style="text-align: right">
          <el-button type="primary" size="small" @click="save">评论</el-button>
        </div>
      </div>

      <!-- 评论列表 -->
      <div>
        <div v-for="item in reviews" :key="item.id" style="border-bottom: 1px solid #ccc; padding: 10px 0">
          <div style="display: flex">
            <div style="width: 100px; text-align: center">
              <!-- 评论人头像 -->
              <el-image :src="item.avatarUrl" style="width: 50px; height: 50px; border-radius: 50%"></el-image>
            </div>
            <div style="flex: 1; font-size: 14px; padding: 5px 0; line-height: 25px">
              <!-- 评论人名称 -->
              <b>{{ item.nickname }}：</b>
              <!-- 评论内容 -->
              <span>{{ item.review }}</span>
              <div style="display: flex; line-height: 20px; margin-top: 5px">
                <div style="width: 200px">
                  <i class="el-icon-time"></i><span style="margin-left: 5px">{{ item.time }}</span>
                </div>
                <div style="text-align: right; flex: 1">
                  <el-button style="margin-left: 5px" type="text" @click="handleReply(item.id)">回复</el-button>
                  <el-button type="text" style="color: red" @click="del(item.id)" v-if="user.id === item.userId">删除</el-button>
                </div>
              </div>
            </div>
          </div>


          <!--  判断item有children才展示  -->
          <div v-if="item.children.length" style="padding-left: 120px;">
            <div v-for="subItem in item.children" :key="subItem.id"  style="background-color: #f0f0f0; padding: 5px 20px">
              <!--  回复列表  -->
              <div style="font-size: 14px; padding: 5px 0; line-height: 25px">
                <div>
                  <b>{{ subItem.nickname }}：</b>
                  <b style="color: #3a8ee6" v-if="subItem.pnickname">@{{ subItem.pnickname }} </b>
                  <span>{{ subItem.review }}</span>
                </div>

                <div style="display: flex; line-height: 20px; margin-top: 5px; padding-left: 5px">
                  <div style="width: 200px;">
                    <i class="el-icon-time"></i><span style="margin-left: 5px">{{ subItem.time }}</span>
                  </div>
                  <div style="text-align: right; flex: 1">
                    <el-button style="margin-left: 5px" type="text" @click="handleReply(subItem.id)">回复</el-button>
                    <el-button type="text" style="color: red" @click="del(subItem.id)">删除</el-button>
                   <!-- <el-button type="text" style="color: red" @click="del(subItem.id)" v-if="user.id === subItem.userId" >删除</el-button> -->
                  </div>

                </div>
              </div>
            </div>
          </div>



        </div>
      </div>
    </div>

    <el-dialog title="回复" :visible.sync="dialogFormVisible" width="50%">
      <el-form label-width="80px" size="small">
        <el-form-item label="回复内容">
          <el-input type="textarea" v-model="reviewForm.reviewReply" autocomplete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false" size="small">取 消</el-button>
        <el-button type="primary" @click="save" size="small">确 定</el-button>
      </div>
    </el-dialog>

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
      pics: [],
      user: localStorage.getItem("user") ? JSON.parse(localStorage.getItem("user")) : {},
      id: this.$route.query.id,
      reviews: [],
      reviewForm: {},
      dialogFormVisible: false,
    };
  },
  created() {
    this.load();
    this.loadReview();
  },
  methods: {
    load() {
      this.request.get("/pic/" + this.id).then((res) => {
        this.pics = res.data;
      });
    },
    loadReview() {
      this.request.get("/review/tree/" + this.id).then((res) => {
        this.reviews = res.data;
      });
    },
    save() {
      this.reviewForm.picId = this.id;
      if (this.reviewForm.reviewReply) {
        this.reviewForm.review = this.reviewForm.reviewReply;
      }
      this.request.post("/review", this.reviewForm).then((res) => {
        if (res.code === "200") {
          this.$message.success("评论成功");
          this.reviewForm = {}; // 初始化评论对象内容
          this.dialogFormVisible = false;
          this.loadReview();
        } else {
          this.$message.error(res.msg);
        }
      });
    },
    del(id) {
      this.request.delete("/review/" + id).then((res) => {
        if (res.code === "200") {
          this.$message.success("删除成功");
          this.loadReview();
        } else {
          this.$message.error("删除失败");
        }
      });
    },
    handleReply(pid) {
      this.reviewForm = { pid: pid};
      this.dialogFormVisible = true;
    },
    goTop() {
      let top = document.documentElement.scrollTop || document.body.scrollTop;
      // 实现滚动效果
      const timeTop = setInterval(() => {
        document.body.scrollTop = document.documentElement.scrollTop = top -= 50;
        if (top <= 0) {
          clearInterval(timeTop);
        }
      }, 20);
    },
  },
};
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
