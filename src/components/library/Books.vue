<template>
  <div>
    <search-bar @onSearch="searchBooks" ref="searchBar"></search-bar>
    <el-row style="height: 500px;">
      <el-tooltip effect="dark" placement="right" style="margin-top: 25px;"
                  v-for="item in books"
                  :key="item.id">
        <p slot="content" style="font-size: 14px;margin-bottom: 6px;">{{item.title}}</p>
        <p slot="content" style="font-size: 13px;margin-bottom: 6px">
          <span>{{item.author}}</span> /
          <span>{{item.date}}</span> /
          <span>{{item.press}}</span>
        </p>
        <p slot="content" style="width: 300px" class="abstract">{{item.abs}}</p>
        <el-card style="width: 145px;margin-bottom: 20px;height: 270px;float: left;margin-right: 15px" class="book"
                 bodyStyle="padding:10px" shadow="hover">
          <div class="cover">
            <img :src="item.cover" alt="封面">
          </div>
          <div class="info">
            <div class="title">
              <a href="">{{item.title}}</a>
            </div>
          </div>
          <div class="author">{{item.author}}</div>
          <div style="padding-left: 107px;float: right;"><i class="el-icon-delete"></i></div>
        </el-card>
      </el-tooltip>
      <edit-form @onSubmit="loadBooks"></edit-form>
    </el-row>
    <el-row style="margin-top: 145px;">
      <el-pagination
        @current-change="changeCurrent"
        :current-page="currentPage"
        :page-size="pageSize"
        :total="total">
      </el-pagination>
    </el-row>
  </div>
</template>

<script>
  import SearchBar from './SearchBar.vue'
  import EditForm from './EditForm.vue'
  import Bus from '../bus.js'
  export default {
    name: 'Books',
    components: {SearchBar,EditForm},
    data () {
      return {
        books: [],
        currentPage: 1,
        pageSize: 10,
        total: 0,
        cid: 0,
        input: ''
      }
    },
    mounted: function () {
      this.loadBooks()
    },
    // 兄弟节点之间的传值 通过bus.js媒介
    created () {
      var _this = this
      Bus.$on('dataChild',(index, currentPage)=>{
        this.cid = index
        this.currentPage = currentPage  //切换cid 置当前页为1
      })
    },
    methods: {
      loadBooks () {
        var _this = this
        // axios 使用 post 发送数据时，默认是直接把 json 放到请求体中提交到后端的
        // 也就是前端请求 Content-Type 变成了 application/json;charset=utf-8
        // 实际后端要求的 'Content-Type': 'application/x-www-form-urlencoded' 为多见
        //所以定义URLSearchParams方式处理
        let param = new URLSearchParams()
        param.append("pageSize", this.pageSize)
        param.append("currentPage", this.currentPage)
        param.append("cid", this.cid)
        param.append("title", this.input)
        this.$axios.post('/pageBooks', param).then(resp => {
          if (resp) {
            _this.books = resp.data.content
            _this.total = resp.data.totalElements
          }
        })
      },
      searchBooks () {
        var _this = this
        _this.input = _this.$refs.searchBar.input
        _this.loadBooks()
        // this.$axios
        //   .get('/search?keywords=' + this.$refs.searchBar.input, { // 获取子组件的属性
        //   }).then(resp => {
        //   if (resp) {
        //     _this.books = resp.data
        //   }
        // })
      },
      changeCurrent (currentPage) {
        this.currentPage = currentPage
        this.loadBooks()
      }
    }
  }
</script>

<style scoped>
  .cover {
    width: 115px;
    height: 172px;
    margin-bottom: 7px;
    overflow: hidden;
    cursor: pointer;
  }

  img {
    width: 115px;
    height: 172px;
    /*margin: 0 auto;*/
  }

  .title {
    font-size: 14px;
    text-align: left;
  }

  .author {
    color: #333;
    width: 102px;
    font-size: 13px;
    margin-bottom: 6px;
    text-align: left;
  }

  .abstract {
    display: block;
    line-height: 17px;
  }

  a {
    text-decoration: none;
  }

  a:link, a:visited, a:focus {
    color: #3377aa;
  }
</style>
