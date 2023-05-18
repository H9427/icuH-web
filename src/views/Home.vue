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
          
          <el-input v-model="name" placeholder="请输入名称" style="width: 200px; margin-left: 5px" :suffix-icon="User"/>
          <el-input v-model="email" placeholder="请输入邮箱" style="width: 200px; margin-left: 5px" :suffix-icon="Message"/>
          <el-input v-model="address" placeholder="请输入地址" style="width: 200px; margin-left: 5px" :suffix-icon="Position"/>
          <button class="btn btn-info btn-sm" style="margin-left: 5px">
            <span>搜索&nbsp;</span>
            <el-icon><Search /></el-icon>
          </button>
          <button class="btn btn-warning btn-sm" style="margin-left: 5px">
            <span>重置&nbsp;</span>
            <el-icon><Refresh /></el-icon>
          </button>
          <button class="btn btn-accent btn-sm" style="margin-left: 5px">
            <span>新增&nbsp;</span>
            <el-icon><CirclePlus /></el-icon>
          </button>
          <button class="btn btn-error btn-sm" style="margin-left: 5px">
            <span>批量删除&nbsp;</span>
            <el-icon><Remove /></el-icon>
          </button>
        </div>

        <!-- 主体-表格内容 -->
        <div style="margin: 10px 0">
          <div class="overflow-x-auto w-full">
            <el-table :data="state.tableDate" stripe border @selection-change="handleSelectionChange">
              <el-table-column type="selection" width="55" />
              <el-table-column prop="name" label="名称"></el-table-column>
              <el-table-column prop="address" label="地址"></el-table-column>
              <el-table-column prop="phone" label="电话"></el-table-column>
              <el-table-column label="操作" width="175px">
                <template #default="scope">
                  <button class="btn btn-accent btn-sm">
                    <span>编辑&nbsp;</span>
                    <el-icon><Edit /></el-icon>
                  </button>
                  <button class="btn btn-error btn-sm" style="margin-left: 5px">
                    <span>删除&nbsp;</span>
                    <el-icon><Delete /></el-icon>
                  </button>
                </template>
              </el-table-column>
            </el-table>
          </div>
        </div>

        <!-- 主体-分页部分 -->
        <div>
          <el-pagination v-model:current-page="pageNum" v-model:page-size="pageSize" small background layout="total, sizes, prev, pager, next ,jumper" :total="50" />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref } from "vue";
import { Document, Menu as IconMenu, Location, Setting, Search, Refresh, CirclePlus,User,Remove,Edit,Delete,Message,Position } from "@element-plus/icons-vue";

const name = ref("");
const email = ref("");
const address = ref("");
const pageNum = ref(1);
const pageSize = ref(2);
const state = reactive({
  tableDate: [
    { name: "admin", address: "南京", phone: "13727712015" },
    { name: "admin", address: "南京", phone: "13727712015" },
    { name: "admin", address: "南京", phone: "13727712015" },
  ],
});

const multipleSelection = ref([]);
const handleSelectionChange = (val) => {
  multipleSelection.value = val;
};


</script>

<style scoped></style>
