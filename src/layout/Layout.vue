<template>
  <div>
    <div>
      <!-- 头部 -->
      <div style="height: 60px; line-height: 60px; border-bottom: 1px sold #ccc; background-color: aliceblue">
        <div style="display: flex">
          <div style="width: 200px; color: dodgerblue; font-weight: bold; padding-left: 20px; font-size: 18px">icuH后台管理系统</div>
          <div style="flex: 1; display: flex">
            <div style="flex: 1">中间</div>
            <div style="width: 200px; text-align: right; padding-right: 10px">头像</div>
          </div>
        </div>
      </div>

      <!-- 主体 -->
      <div style="display: flex">
        <!-- 左侧导航栏 -->
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
          <RouterView />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { RouterView } from "vue-router";
import { Document, Menu as IconMenu, Location, Setting } from "@element-plus/icons-vue";

export default {
  data() {
    return {};
  },
};
</script>

<style scoped></style>
