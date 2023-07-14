<template>
  <div style="user-select: none;">
    <!-- 头部区域 -->
    <div style="height: 60px; line-height: 60px; background-color: white; margin-bottom: 2px; display: flex ">
      <div style="width: 600px">
        <!-- <img src="@/assets/image/logo.png" alt="" style="width: 80px; position: relative; top: 15px; left: 10px">
        <span style="margin-left: 20px; font-size: 24px">残疾人就业保障金征收及使用监管系统</span> -->
      </div>
      
      
      <div style="flex: 1; text-align: right; padding-right: 20px">
      </div>
    </div>

    <!-- 侧边栏和主体 -->
    <div style="display: flex">

      <!-- 侧边栏导航 -->
      <div ref="sideBar" class="sidebar">
        <el-button class="lock" circle @click="toggleSidebar" size="large">

          <Pushpin v-if="isMenuExpanded" theme="filled" size="24" fill="#409eff" :strokeWidth="1" />
          <Pushpin v-else theme="filled" size="24" fill="#dbe0e2" :strokeWidth="1" />
        </el-button>
        <el-menu :default-active="$route.path" router class="el-menu-demo" style="margin-bottom: 10px"
          :collapse="!(isMenuExpanded || isMouseInside)" >
          <el-menu-item index="/">
            <template #title>
              <span>首页</span>
            </template>
            <template #>
              <HomeTwo theme="filled" size="24" fill="#333" :strokeWidth="1" />
            </template>
          </el-menu-item>
        </el-menu>
      </div>

      <!-- 主体数据 -->
      <!-- width: 0; 可以限制容器的宽度，不被子元素无限撑开-->
      <div style="flex: 1; width: 0; background-color: white; padding: 10px">
        <router-view />
      </div>
    </div>
  </div>
  
</template>



<script setup>

import { ref, onMounted} from 'vue';
import {Pushpin} from '@icon-park/vue-next';
const sideBar = ref(null);
const isMouseInside = ref(false);
const isMenuExpanded = ref(false);


const handleMouseEnter = () => {
  if (isMenuExpanded.value) {
    return;
  }
  isMouseInside.value = true;
};

const handleMouseLeave = () => {
  if (isMenuExpanded.value) {
    return;
  }
  isMouseInside.value = false;
};
const toggleSidebar = () => {
  isMenuExpanded.value = !isMenuExpanded.value;
  const sidebar = document.querySelector('.sidebar');
  if (isMenuExpanded.value) {
    sidebar.classList.remove('collapse');
    sidebar.classList.add('expanded');
  } else {
    sidebar.classList.remove('expanded');
    sidebar.classList.add('collapse');
  }
}
onMounted(() => {
  sideBar.value.addEventListener('mouseenter', handleMouseEnter);
  sideBar.value.addEventListener('mouseleave', handleMouseLeave);
});

// onUnmounted(() => {
//   sideBar.value.removeEventListener('mouseenter', handleMouseEnter);
//   sideBar.value.removeEventListener('mouseleave', handleMouseLeave);
// });
</script>

<style scoped>
.sidebar {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 64px;
  min-height: calc(100vh - 62px);
  overflow: hidden;
  margin-right: 2px;
  background-color: white;
  transition: width 0.3s ease-in-out;
}

.sidebar:hover {
  width: 200px;
}

.expanded {
  width: 200px;
}

.collapse {
  width: 64px;
}

.lock {
  top: 10px;
  background: #fff;
  border-color: #cbcbcd;
  color: #505255;
}

.lock:hover {
  background: #ecf5ff;
  border-color: #c6e2ff;
  color: #409eff;
}

.el-menu {
  border-right: none;
  text-decoration: none;
}
</style>