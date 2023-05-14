<template>
  <!-- 左边小按钮 -->
  <div class="navbar bg-base-100 flex-1">
    <div class="navbar-start">
      <div class="dropdown">
        <label tabindex="0" class="btn btn-ghost btn-circle">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h7" />
          </svg>
        </label>
        <ul tabindex="0" class="menu menu-compact dropdown-content mt-3 p-2 shadow bg-base-100 rounded-box w-52">
          <li><a>Homepage</a></li>
          <li><a>xxxpage</a></li>
        </ul>
      </div>
      <div>
        <a class="btn btn-ghost normal-case text-xl" @click="this.$router.push('/login')">icuH</a>
      </div>
    </div>
    <input type="text" placeholder="Search here" class="input input-bordered input-sm w-full max-w-xs bg-slate-50" />
    <div class="navbar-end">
      <a class="btn login" @click="this.$router.push('/login')">Login</a>
    </div>
  </div>
</template>


<script>
export default {
  name: "Index",
  components: {},

}
</script>

<style scoped>
.login {
  width: 110px;
}
</style>
