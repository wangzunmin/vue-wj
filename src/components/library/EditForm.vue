<template>
  <div>
    <i class="el-icon-circle-plus-outline"  @click="dialogFormVisible = true"></i>
    <el-dialog title="添加图书" :visible.sync="dialogFormVisible">
      <el-form v-model="form">
        <el-form-item label="图书地址" :label-width="formLabelWidth">
          <el-input v-model="form.cover" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="书名" :label-width="formLabelWidth">
          <el-input v-model="form.title" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="作者" :label-width="formLabelWidth">
          <el-input v-model="form.author" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="出版日期" :label-width="formLabelWidth">
          <el-input v-model="form.date" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="出版社" :label-width="formLabelWidth">
          <el-input v-model="form.press" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="简介" :label-width="formLabelWidth">
          <el-input v-model="form.abs" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="分类" :label-width="formLabelWidth">
          <el-select v-model="form.cid" placeholder="请选择" style="width: 515px;">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value">
            </el-option>
          </el-select>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="submit">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
  export default {
    name: 'EditForm',
    data () {
      return {
        formLabelWidth: '120px',
        dialogFormVisible: false,
        form: {
          cover: '',
          title: '',
          author: '',
          date: '',
          press: '',
          abs: '',
          cid: ''
        },
        options: [
          {
            value: '1',
            label: '文学'
          },
          {
            value: '2',
            label: '流行'
          },
          {
            value: '3',
            label: '文化'
          },
          {
            value: '4',
            label: '生活'
          },
          {
            value: '5',
            label: '经管'
          },
          {
            value: '6',
            label: '科技'
          }
        ]
      }
    },
    methods: {
      submit() {
        this.$axios
          .post('/add', {
            cover: this.form.cover,
            title: this.form.title,
            author: this.form.author,
            date: this.form.date,
            press: this.form.press,
            abs: this.form.abs,
            cid: this.form.cid
          }).then(resp => {
          if (resp) {
            this.dialogFormVisible = false
            this.form.cover=''
            this.form.title=''
            this.form.author=''
            this.form.date=''
            this.form.press=''
            this.form.abs=''
            this.form.cid=''
            this.$emit('onSubmit')
          }
        })
      }
    }
  }
</script>

<style scoped>
  .el-icon-circle-plus-outline {
    margin: 50px 0 0 20px;
    font-size: 100px;
    float: left;
    cursor: pointer;
  }
</style>
