<template>
  <div>
    <el-input style="width: 40%;" v-model="input" placeholder="搜索"></el-input>
    <el-button style="position: absolute;margin-left: 15px;" type="primary" @click="searchBook">搜索</el-button>
  </div>
</template>

<script>
  export default {
    name: 'SearchBar',
    data () {
      return {
        input: ''
      }
    },
    methods: {
      searchBook () {
        this.$emit('onSearch') // 联系父组件的 触发父组件的自定义事件
      }
    }
  }
</script>

<style scoped>

</style>
