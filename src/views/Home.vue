<template>
  <!-- 头部 -->
  <div>
    <div style="height: 60px; line-height: 60px; border-bottom: 1px sold #ccc; background-color: aliceblue">
      <div style="display: flex">
        <div style="width: 200px; color: dodgerblue; font-weight: bold; padding-left: 20px; font-size: 18px">icuH后台管理系统</div>
        <div style="flex: 1; display: flex">
          <div style="flex: 1">中间</div>
          <div style="width: 200px; text-align: right; padding-right: 10px">头像</div>
        </div>
      </div>
    </div>

    <!-- 左侧导航栏 -->
    <div style="display: flex">
      <div style="width: 200px; min-height: calc(100vh - 60px); border-hight: 1px solid #ccc">
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
          <el-input v-model="name" placeholder="请输入名称" style="width: 300px; margin-left: 5px" />
          <el-input v-model="name" placeholder="请输入名称" style="width: 300px; margin-left: 5px" />
          <button class="btn btn-outline btn-info btn-sm" style="margin-left: 5px">
            搜索&nbsp;
            <el-icon><Search /></el-icon>
          </button>
        </div>

        <div style="margin: 10px 0">
          <div class="overflow-x-auto w-full">
            <table class="table w-full">
              <!-- head -->
              <thead>
                <tr>
                  <th>
                    <label>
                      <input type="checkbox" class="checkbox" />
                    </label>
                  </th>
                  <th>Name</th>
                  <th>Job</th>
                  <th>Favorite Color</th>
                  <th></th>
                </tr>
              </thead>
              <tbody>
                <!-- row 1 -->
                <tr>
                  <th>
                    <label>
                      <input type="checkbox" class="checkbox" />
                    </label>
                  </th>
                  <td>
                    <div class="flex items-center space-x-3">
                      <div class="avatar">
                        <div class="mask mask-squircle w-12 h-12">
                          <img src="../assets/img/logo.png" alt="Avatar Tailwind CSS Component" />
                        </div>
                      </div>
                      <div>
                        <div class="font-bold">Hart Hagerty</div>
                        <div class="text-sm opacity-50">United States</div>
                      </div>
                    </div>
                  </td>
                  <td>
                    Zemlak, Daniel and Leannon
                    <br />
                    <span class="badge badge-ghost badge-sm">Desktop Support Technician</span>
                  </td>
                  <td>Purple</td>
                  <th>
                    <button class="btn btn-ghost btn-xs">details</button>
                  </th>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref } from "vue";
import { Document, Menu as IconMenu, Location, Setting, Search } from "@element-plus/icons-vue";

const name = ref("");
const state = reactive({
  tableDate: [
    { name: "admin", address: "南京", phone: "13727712015" },
    { name: "admin", address: "南京", phone: "13727712015" },
    { name: "admin", address: "南京", phone: "13727712015" },
],
});
</script>

<style scoped></style>
