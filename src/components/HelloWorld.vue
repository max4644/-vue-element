<template>
  <div>
<!--    搜索查询-->
    <el-form :inline="true" :model="filters" ref="filters">
      <el-form-item prop="name" label="客户名称" size="small">
        <el-input type="text" v-model="filters.name" placeholder="请输入客户名称" clearable @clear="clearListPage">
          <i slot="prefix" class="el-input__icon el-icon-search"></i>
          <el-button type="primary" slot="append" @click="listPage">查询</el-button>
        </el-input>
      </el-form-item>
    </el-form>
    <el-button size="mini" type="primary" @click="add">添加</el-button>
<!--    表格-->
    <el-table
      :data="tableData"
      style="width: 100%"
    border>
      <el-table-column
        label="日期"
        prop="date">
      </el-table-column>
      <el-table-column
        label="姓名"
        prop="name">
        <template slot-scope="scope">
          {{ scope.row.name }}
<!--          <el-popover trigger="hover" placement="top">-->
<!--            <p>姓名: {{ scope.row.name }}</p>-->
<!--            <p>住址: {{ scope.row.address }}</p>-->
<!--            <div slot="reference" class="name-wrapper">-->
<!--              <el-tag size="medium">{{ scope.row.name }}</el-tag>-->
<!--            </div>-->
<!--          </el-popover>-->
        </template>
      </el-table-column>
      <el-table-column label="操作">
        <template slot-scope="scope">
          <el-button
            size="mini"
            @click="change(scope.$index, scope.row)">编辑</el-button>
          <el-button
            size="mini"
            type="danger"
            @click="del(scope.$index, scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
<!--    弹窗-->
    <el-dialog
      :title="titleDialog"
      :visible.sync="showDialog" @close="closeDialog">
      <el-form :model="addForm" ref="addForm" :rules="addRules"  label-width="100px">
        <el-form-item prop="name" label="客户名称" >
          <el-input v-model="addForm.name" size="small" placeholder="请选择"></el-input>
        </el-form-item>
        <el-form-item prop="age" label="客户年龄" size="small">
          <el-input-number v-model="addForm.age" :min="1" size="small" style="width: 100%;" placeholder="请选择"></el-input-number>
        </el-form-item>
        <el-form-item prop="sex" label="客户性别" size="small">
          <el-select v-model="addForm.sex" placeholder="请选择" style="width: 100%;" size="small">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value">
            </el-option>
          </el-select>
        </el-form-item>
        <el-form-item prop="birth" label="客户出生日期" size="small">
          <el-date-picker type="datetime" placeholder="选择日期" v-model="addForm.birth" style="width: 100%;" size="mini" value-format="yyyy-MM-dd HH:mm:ss"></el-date-picker>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
    <el-button size="mini" @click="showDialog = false">取 消</el-button>
    <el-button size="mini" type="primary"  @click="submitForm(titleDialog)" :disabled="saveBtn">确 定</el-button>
  </span>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      filters: {
        name: '',
      },
      tableData: [{
        date: '2016-05-02',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }],
      showDialog: false,
      addForm: {
        name: '',
        age: 1,
        sex: '',
        birth: ''
      },
      addRules: {
        name: [ { required: true, message: '请输入', trigger: 'blur' }],
        age: [ { required: true, message: '请输入', trigger: 'blur' }],
        sex: [ { required: true, message: '请选择', trigger: 'change' }],
        birth: [ { required: true, message: '请选择', trigger: 'change' }],
      },
      options: [{
        value: '0',
        label: '男'
      }, {
        value: '1',
        label: '女'
      }],
      saveBtn: false,
      titleDialog: '添加'
    }
  },
  methods: {
    listPage () {
      console.log('查询页面' + this.filters)
    },
    clearListPage () {
      this.filters = {
        name: '',
      }
      this.listPage()
    },
    del(index, row) {
      this.$confirm('此操作将删除该数据, 是否继续?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        this.$message({
          type: 'success',
          message: '删除成功'
        });
      }).catch(() => {
        this.$message({
          type: 'info',
          message: '已取消删除'
        });
      })
    },
    // 提交弹窗的表格
    submitForm(name) {
      this.saveBtn = true
      if (name === '添加') {
        console.log('添加')
        this.insert(this.addForm)
      } else {
        console.log('编辑')
        this.update(this.addForm)
      }
      setTimeout(() => {
        this.saveBtn = false
      }, 1500)
    },
    insert(addForm) {
      // 正式添加
      this.$refs.addForm.validate((valid) => {
        if (valid) {
          console.log('submit!');
        } else {
          console.log('error submit!!');
          return false;
        }
      });
    },
    update(addForm) {
      // 正式编辑
    },
    add() {
      this.showDialog = true
      this.titleDialog = '添加'
    },
    change() {
      this.showDialog = true
      this.titleDialog = '编辑'
    },
    closeDialog() {

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
