<template>
    <div class="login-container">
      <div class="login-image">
        <img src="../assets/img/bg.jpg" alt="Login Image" />
      </div>
      <div class="login-form">
        <h2 class="login-title" style="padding-left: 10%;">Welcome to icuH</h2>
        <div>
          <div class="form-control">
            <input type="text" v-model="user.name" placeholder="Username" class="input" />
          </div>
          <div class="form-control">
            <input type="password" v-model="user.password" placeholder="Password" class="input" />
          </div>
          <div class="form-control">
            <input type="password" v-model="user.password" placeholder="Conform Password" class="input" />
          </div>
          <button type="submit" class="btn btn-primary">Log In</button>
        </div>
  
        <div class="login-links">
          <a  @click="this.$router.push('/login')" class="link">Sign in to icuH</a>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, reactive } from "vue";
  
  const user = reactive({
    name: "张三",
  });
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
    width: 120%;
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
    width: 120%;
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
  