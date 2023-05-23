<template>
  <div class="login-container">
    <div class="login-image">
      <img src="../assets/img/bg1.jpg" alt="Login Image" />
    </div>
    <div class="login-form">
      <h2 class="login-title" style="padding-left: 10%">Sign in to icuH</h2>
      <div style="margin-right: 10%">
        <div class="form-control">
          <input type="text" v-model="user.name" placeholder="Email or Username" class="input" />
        </div>
        <div class="form-control">
          <input type="password" v-model="user.password" placeholder="Password" class="input" />
        </div>
        <button type="submit" class="btn btn-primary" @click="login">Log In</button>
      </div>

      <div class="login-links">
        <a @click="this.$router.push('/register')" class="link">Register for icuH</a>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ElMessage,ElNotification } from "element-plus";
import { ref, reactive } from "vue";
import request from "../request.js";

const user = reactive({
  name: "张三",
});

const login = () => {
  if (!user.name || !user.password) {
    ElNotification({
      type: "error",
      message: "请输入用户名或密码",
    });
  } else {
    // 执行登录逻辑
    request.post("/user/login").then((res) => {
      if (res.code === '200') {
        ElNotification({
          type: "success",
          message: "请输入用户名或密码",
        });
      } else {
        ElNotification({
          type: "error",
          message: "请输入用户名或密码",
        });
      }
    });
  }
};
</script>

<style>
.login-container {
  display: flex;
  height: 100vh;
  background-color: #f2f5f9;
}

.login-image {
  width: 70%;
  overflow: hidden;
}

.login-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.login-form {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 40px;
  border-radius: 8px;
  background-color: #ffffff;
  box-shadow: 0 1px 4px rgba(0, 0, 0, 0.1);
}

.login-title {
  text-align: center;
  font-size: 24px;
  font-weight: bold;
  color: #333333;
  margin-bottom: 30px;
}

.form-control {
  margin-bottom: 20px;
  width: 100%;
}

.input {
  width: 140%;
  padding: 12px;
  border: 1px solid #e0e6ed;
  border-radius: 3px;
  background-color: #f5f8fa;
  color: #333333;
  transition: border-color 0.3s ease;
}

.input:focus {
  outline: none;
  border-color: #1e90ff;
  box-shadow: 0 0 0 2px rgba(30, 144, 255, 0.2);
}

.btn {
  width: 140%;
  padding: 12px 0;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  font-weight: bold;
  border-radius: 3px;
  transition: background-color 0.3s ease;
  cursor: pointer;
  background-color: #1e90ff;
  color: #ffffff;
  border: none;
}

.btn:hover {
  background-color: #007bff;
}

.login-links {
  margin-top: 20px;
  text-align: center;
  font-size: 14px;
}

.link {
  color: #1e90ff;
  text-decoration: none;
}

.separator {
  margin: 0 4px;
  color: #999999;
}
</style>
