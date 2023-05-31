<body>
  <script src="https://cdn.staticfile.org/vue/2.6.9/vue.js"></script>
</body>

<template>
  <div id='app' class="container">
    <img src="../../public/loginRegister/bg.jpg"/>
    <div class="panel">
      <div class="content login">

        <div class="switch">
          <span :class='{"active": active === "login"}' @click="$router.push('/login')">Login</span>
          <span> / </span>
          <span :class='{"active": active === "register"}' @click="$router.push('/register')">Register</span>
        </div>
        <div class='form' id="fromLogin">
          <el-form :model="user" :rules="rules" ref="userForm">
            <div class="input"><input :class='{ hasValue: user.username }' v-model='user.username' type="text" name="username" id="username" /><label >用户名</label></div>
            <div class="input"><input :class='{ hasValue: user.password }' v-model='user.password' type="password" name="password" id="password" /><label>密码</label></div>
            <el-button size="small" autocomplete="off" @click="login">Login</el-button>
          </el-form>
        </div>
        <el-button size="small" style="margin-left: 35%; margin-top: 70%" autocomplete="off" @click="frontHome">Main</el-button>
      </div>
    </div>
  </div>
</template>

<script>
import {setRoutes} from "@/router";

export default {
  name: "Login",
  data() {
    return {
      active: 'login',
      user: {username: '', password: '', },
      rules: {
        username: [
          // {required: true, message: 'Please enter your username', trigger: 'blur'},
          {required: true, message: ' ', trigger: 'blur'},
          {min: 3, max: 10, message: '长度在 3 到 5 个字符', trigger: 'blur'}
        ],
        password: [
          {required: true, message: ' ', trigger: 'blur'},
          {min: 1, max: 20, message: '长度在 1 到 20 个字符', trigger: 'blur'}
        ],
      }
    }
  },
  methods: {
    login() {
      this.$refs['userForm'].validate((valid) => {
        if (valid) {  // 表单校验合法
          this.request.post("/user/login", this.user).then(res => {
            if(res.code === '200') {
              localStorage.setItem("user", JSON.stringify(res.data))//存储用户信息
              localStorage.setItem("menus", JSON.stringify(res.data.menus))
              //动态设置当前用户的路由
              setRoutes()

              this.$message.success("登陆成功")

              if(res.data.role === 'ROLE_USER') {
                this.$router.push("/front/home")
              } else {
                this.$router.push("/home")
              }
            } else {
              this.$message.error(res.msg)
            }
          })
        }
      });
    },
    frontHome() {
      this.$router.push("/front/home")
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

body {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: miaowu;
  background: linear-gradient(45deg, rgb(181, 154, 254), rgb(245, 189, 253)) fixed;
}

.container {
  position: relative;
  width: 70rem;
}

.container img {
  width: 70rem;
}

.switch span {
  color: #ccc;
  font-size: 1.4rem;
  cursor: pointer;
}

.switch span.active {
  color: rgb(181, 154, 254);
}

.panel {
  width: 30%;
  margin: 10rem 0 0;
  position: absolute;
  right: 0;
  top: 0;

  display: flex;
  justify-content: center;
}

.form {
  width: 12rem;
  margin: 3rem 0 0;
}

.form .input {
  position: relative;
  opacity: 1;
  height: 2rem;
  width: 100%;
  margin: 2rem 0;
  transition: .4s;
}

.input input {
  outline: none;
  width: 100%;
  border: none;
  border-bottom: .1rem solid rgb(181, 154, 254);
  position: relative;
  line-height: 35px;
  background: transparent;
  z-index: 1;
}

.input label {
  position: absolute;
  left: 0;
  top: 20%;
  font-size: 1.2rem;
  color: rgb(129, 101, 207);
  transition: .3s;
}

/* fixbug for IMBIT（1448214956） */
.hasValue ~ label, input:focus ~ label {
  top: -50%;
  font-size: .9rem;
}



.form span {
  display: block;
  color: rgb(110, 89, 167);
  font-size: .8rem;
  cursor: pointer;
}

.form button {
  border: none;
  outline: none;
  margin: 2.5rem 0 0;
  width: 100%;
  height: 3rem;
  border-radius: 3rem;
  background: linear-gradient(90deg, rgb(181, 154, 254), rgb(245, 189, 253));
  box-shadow: 0 0 8px rgb(181, 154, 254);
  cursor: pointer;
  color: white;
  font-family: miaowu;
}

</style>
