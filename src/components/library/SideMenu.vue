<template>
  <el-menu
    class="categories"
    :default-active="activeIndex"
    @select="handleSelect"
    active-text-color="red">
    <el-menu-item index="0">
      <i class="el-icon-menu"></i>
      <span slot="title">全部</span>
    </el-menu-item>
    <el-menu-item index="1">
      <i class="el-icon-menu"></i>
      <span slot="title">文学</span>
    </el-menu-item>
    <el-menu-item index="2">
      <i class="el-icon-menu"></i>
      <span slot="title">流行</span>
    </el-menu-item>
    <el-menu-item index="3">
      <i class="el-icon-menu"></i>
      <span slot="title">文化</span>
    </el-menu-item>
    <el-menu-item index="4">
      <i class="el-icon-menu"></i>
      <span slot="title">生活</span>
    </el-menu-item>
    <el-menu-item index="5">
      <i class="el-icon-menu"></i>
      <span slot="title">经管</span>
    </el-menu-item>
    <el-menu-item index="6">
      <i class="el-icon-menu"></i>
      <span slot="title">科技</span>
    </el-menu-item>
  </el-menu>
</template>

<script>
  import Bus from '../bus.js'
  export default {
    name: 'SideMenu',
    data () {
      return {
        activeIndex: '0'
      }
    },
    methods: {
      handleSelect (index, indexPath) {
        this.activeIndex = index //cid
        Bus.$emit('dataChild',index, 1) // 兄弟节点之间的传值
        this.$emit("indexSelect")
      }
    }
  }
</script>

<style scoped>
  .categories {
    position: fixed;
    margin-left: 45%;
    left: -600px;
    top: 100px;
    width: 150px;
  }
</style>
