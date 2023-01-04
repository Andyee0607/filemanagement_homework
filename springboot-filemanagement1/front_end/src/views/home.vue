<template>
  <el-container class="layout-container-demo" style="height: 700px">
    <el-aside width="250px">
      <el-scrollbar>
        <el-sub-menu index="1">
          <template #title></template>
          <el-menu-item-group>
            <el-menu-item index="1-1"><el-icon><DocumentRemove /></el-icon>文件</el-menu-item>
            <el-menu-item index="1-2"><el-icon><PictureFilled /></el-icon>相册</el-menu-item>
            <el-menu-item index="1-3"><el-icon><Star /></el-icon>收藏夹</el-menu-item>
            <el-menu-item index="1-4"><el-icon><Earth /></el-icon>共享文件</el-menu-item>
            <el-menu-item index="1-5"><el-icon><Share /></el-icon>我的分享</el-menu-item>
            <el-menu-item index="1-6"><el-icon><Bin/></el-icon>回收站</el-menu-item>
          </el-menu-item-group>
        </el-sub-menu>
      </el-scrollbar>
    </el-aside>

    <el-container>
      <el-header style="text-align: right; font-size: 12px;width:1000px">
        <div class="toolbar">
          <el-dropdown>
            <el-icon style="margin-right: 20px; margin-top: 1px"
            ><setting
            /></el-icon>
            <template #dropdown>
              <el-dropdown-menu>
                <el-dropdown-item><el-icon><CirclePlus /></el-icon></el-dropdown-item>
              </el-dropdown-menu>
            </template>
          </el-dropdown>
          <span>文件</span>
        </div>
      </el-header>

      <el-main>
        <el-carousel indicator-position="outside">
          <el-carousel-item v-for="item in 4" :key="item" >
            <h3 text="2xl" justify="center">{{ item }}</h3>
          </el-carousel-item>
        </el-carousel>
      </el-main>
      <el-bottom>
        <el-menu-item-group>
          <el-item index="1"><el-icon @click="$emit"><Download /></el-icon></el-item>
          <el-item index="2"><el-icon @click="$isServer"><Star /></el-icon></el-item>
          <el-item index="3"><el-icon @click="$delete"><Delete /></el-icon></el-item>
          <elu-item index="4"><el-icon @click="$parent"><Earth /></el-icon></elu-item>
          <el-item index="5"><el-icon @click="close()"><CircleCloseFilled /></el-icon></el-item>
      </el-bottom>
    </el-container>
  </el-container>
</template>

<script>
export default {
  name: "home"
}
</script>

<style scoped>
.layout-container-demo .el-header {
  position: relative;
  background-color: var(--el-color-primary-light-7);
  color: var(--el-text-color-primary);
}
.layout-container-demo .el-aside {
  color: var(--el-text-color-primary);
  background: var(--el-color-primary-light-8);
}
.layout-container-demo .el-menu {
  border-right: none;
}
.layout-container-demo .el-main {
  padding: 0;
}
.layout-container-demo .toolbar {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  right: 20px;
}
</style>
