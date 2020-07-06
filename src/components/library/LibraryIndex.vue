<template>
  <el-container>
    <el-aside style="width: 200px;margin-top: 20px">
      <switch></switch>
      <side-menu @indexSelect="selectIndex" ref="sideMenu"></side-menu>
    </el-aside>
    <el-main>
      <books ref="booksArea"></books>
    </el-main>
  </el-container>
</template>

<script>
  import SideMenu from './SideMenu'
  import Books from './Books'
  export default {
    name: 'LibraryIndex',
    components: {SideMenu, Books},
    methods: {
      selectIndex () {
        var _this = this
        // this.cid = _this.$refs.sideMenu.activeIndex  //组件之间的通信
        // cid传递到books.vue中
        _this.$refs.booksArea.loadBooks()
        // 根据cid 调用api接口查询该目录下的数据
        // var url = "categories/" + cid + "/books"
        // this.$axios.get(url).then(resp => {
        //   if (resp) {
        //     _this.$refs.booksArea.books = resp.data
        //   }
        // })
      }
    }
  }
</script>

<style scoped>

</style>
