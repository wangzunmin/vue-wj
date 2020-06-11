<template>
  <el-container>
    <el-aside style="width: 200px;margin-top: 20px">
      <switch></switch>
      <side-menu></side-menu>
    </el-aside>
    <el-main>
      <books></books>
    </el-main>
  </el-container>
</template>

<script>
  import SideMenu from './SideMenu'
  import Books from './Books'
  export default {
    name: 'LibraryIndex',
    components: {SideMenu,Books}
  }
</script>

<style scoped>

</style>
