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
    <el-row>
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
  export default {
    name: 'Books',
    components: {SearchBar,EditForm},
    data () {
      return {
        books: [],
        currentPage: 1,
        pageSize: 1,
        total: 0
      }
    },
    mounted: function () {
      this.loadBooks()
    },
    methods: {
      loadBooks () {
        var _this = this
        this.$axios.get('/pageBooks?pageSize=' + this.pageSize + '&currentPage=' + this.currentPage).then(resp => {
          if (resp) {
            _this.books = resp.data.content
            _this.total = resp.data.totalPages
          }
        })
      },
      searchBooks () {
        var _this = this
        this.$axios
          .get('/search?keywords=' + this.$refs.searchBar.input, { // 获取子组件的属性
          }).then(resp => {
          if (resp) {
            _this.books = resp.data
          }
        })
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
