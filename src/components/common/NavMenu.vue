<template>
  <el-menu
    :default-active="'/index'"
    router
    class="el-menu-demo"
    mode="horizontal"
    background-color="#545c64"
    text-color="#fff"
    active-text-color="#ffd04b">
    <el-menu-item v-for="(item,i) in navList" :key="i" :index="item.name">
      {{ item.navItem }}
    </el-menu-item>
  </el-menu>
</template>

<script>
  export default {
    name: 'NavMenu',
    data () {
        return {
          navList: [
            {name: '/index', navItem: '首页'},
            {name: '/jotter', navItem: '笔记本'},
            {name: '/library', navItem: '图书馆'},
            {name: '/admin', navItem: '个人中心'}
          ]
      }
    }
  }
</script>

<style scoped>
  .el-menu-demo{
    margin-top: -54px;
  }
</style>
