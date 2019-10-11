<template>
    <div>
        <!--    搜索查询-->
        <el-form :inline="true" :model="filters" ref="filters">
            <el-form-item prop="name" label="客户名称" size="small">
                <el-input type="text" v-model.trim="filters.name" placeholder="请输入客户名称" clearable
                          @clear="clearListPage">
                    <i slot="prefix" class="el-input__icon el-icon-search"></i>
                    <el-button type="primary" slot="append" @click="listPage">查询</el-button>
                </el-input>
            </el-form-item>
        </el-form>
        <el-button size="mini" type="primary" @click="addTable">添加</el-button>

        <!--      另一种风格搜索查询 搜索在最右侧 并且带重置-->
        <el-form label-position="top" :model="filters" ref="filters">
            <el-row>
                <el-col :span="8">
                    <el-form-item label="Full Name" size="small">
                        <el-input type="text" v-model="filters.name" placeholder="Please Input" clearable
                                  @clear="clearListPage">
                        </el-input>
                    </el-form-item>
                </el-col>
                <el-col :span="3">
                    <el-form-item label="Sex" size="small">
                        <el-select v-model="filters.name" clearable placeholder="Please Select">
                            <el-option value="dada" label="dada"></el-option>
                        </el-select>
                    </el-form-item>
                </el-col>
                <el-col :span="3">
                    <el-form-item label="Date of Birth" size="small">
                        <el-date-picker type="datetime" placeholder="Please Select" v-model="filters.name"
                                        style="width: 19%;margin-right: 5px;" size="mini"
                                        value-format="yyyy-MM-dd HH:mm:ss"></el-date-picker>
                    </el-form-item>
                </el-col>
                <el-form-item label="" size="small" class="marT35 floatR">
                    <el-button type="primary" @click="searchData">SEARCH</el-button>
                    <el-button @click="resetData">RESET</el-button>
                </el-form-item>
            </el-row>
        </el-form>

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
            </el-table-column>
            <el-table-column
                    label="Status"
                    prop="date">
                <template slot-scope="scope">
                    <el-switch
                            v-model="scope.row.status"
                            active-color="#308CE3"
                            inactive-color="#ccc"
                            :active-value="'1'"
                            :inactive-value="'0'"
                            @change="changeSwitch($event,scope.row)">
                    </el-switch>
                </template>
            </el-table-column>
            <el-table-column label="操作">
                <template slot-scope="scope">
                    <el-button type="text"
                               size="mini"
                               @click="editTable(scope.$index, scope.row)">Edit
                    </el-button>
                    <el-button type="text"
                               size="mini"
                               @click="viewTable(scope.$index, scope.row)">View
                    </el-button>
                    <el-button type="text"
                               size="mini"
                               @click="deleteTable(scope.$index, scope.row)">Delete
                    </el-button>
                </template>
            </el-table-column>
        </el-table>
        <!--    弹窗-->
        <el-dialog
                :title="titleDialog"
                :visible.sync="showDialog" @close="closeDialog">
            <el-form :model="form" ref="forms" :rules="rules" label-width="100px">
                <el-form-item prop="name" label="客户名称">
                    <el-input v-model="form.name" size="small" placeholder="请选择" :disabled="showInputs"></el-input>
                </el-form-item>
                <el-form-item prop="age" label="客户年龄" size="small">
                    <el-input-number v-model="form.age" :min="1" size="small" style="width: 100%;"
                                     placeholder="请选择" :disabled="showInputs"></el-input-number>
                </el-form-item>
                <el-form-item prop="sex" label="客户性别" size="small">
                    <el-select v-model="form.sex" placeholder="请选择" style="width: 100%;" size="small" :disabled="showInputs">
                        <el-option
                                v-for="item in options"
                                :key="item.value"
                                :label="item.label"
                                :value="item.value">
                        </el-option>
                    </el-select>
                </el-form-item>
                <el-form-item prop="birth" label="客户出生日期" size="small">
                    <el-date-picker type="datetime" placeholder="选择日期" v-model="form.birth" style="width: 100%;"
                                    size="mini" value-format="yyyy-MM-dd HH:mm:ss"></el-date-picker>
                </el-form-item>
            </el-form>
            <div slot="footer" class="dialog-footer">
                <el-button type="primary" size="small" @click="saveDialog(titleDialog)" v-show="!showInputs" :disabled="showSaveBtn">SAVE</el-button>
                <el-button  @click="showDialog = false">CLOSE</el-button>
            </div>
        </el-dialog>
    </div>
</template>

<script>
  export default {
    name: 'HelloWorld',
    data() {
      return {
        filters: {
          page: 1,
          pageSize: 10
        },
        tableData: [{
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }],
        showDialog: false,
        form: {
          name: '',
          age: 1,
          sex: '',
          birth: ''
        },
        rules: {
          name: [{required: true, message: '请输入', trigger: 'blur'}],
          age: [{required: true, message: '请输入', trigger: 'blur'}],
          sex: [{required: true, message: '请选择', trigger: 'change'}],
          birth: [{required: true, message: '请选择', trigger: 'change'}],
        },
        options: [{
          value: '0',
          label: '男'
        }, {
          value: '1',
          label: '女'
        }],
        saveBtn: false,
        titleDialog: '添加',
        showSaveBtn: false,
        showInputs: false,
      }
    },
    methods: {
      listPage() {
        console.log('查询页面' + this.filters)
      },
      // 每页条数
      handleSizeChange(val) {
        this.filters.pageSize = val
        this.listPage()
      },
      // 当前页
      handleCurrentChange(val) {
        this.filters.page = val
        this.listPage()
      },
      // 重置搜索条件
      resetData() {
        this.filters = this.$options.data().filters
        this.listPage()
      },
      clearListPage() {
      },
      // 查询数据
      searchData() {
        this.listPage()
      },
      // 查询单条
      getInfoById(ids) {
        this.$http.get('', {
          params: {
            id: ids
          }
        }).then((res) => {
          if (res.data.status === 200) {
            this.form = res.data.data
            this.showDialog = true
          } else {
            this.erFn(res.data.msg)
          }
        }).catch((error) => {
          this.erFn(error);
        })
      },
      // 增加表格数据
      addTable() {
        this.titleDialog = 'Add'
        this.showDialog = true
      },
      // 修改表格数据
      editTable(index, row) {
        this.titleDialog = 'Edit'
        this.getInfoById(row.id)
      },
      // 查看表格数据
      viewTable(index, row) {
        this.titleDialog = 'View'
        this.getInfoById(row.id)
      },
      // 删除表格数据
      deleteTable(index, row) {
        this.$confirm('Do you confirm deletion?', 'Delete', {
          confirmButtonText: 'Yes',
          cancelButtonText: 'No',
          type: 'warning'
        }).then(() => {
          this.$http.get('', {
            params: {

            }
          }).then((res) => {
            if (res.data.status === 200) {
              this.suFn(res.data.msg)
              this.listPage()
            } else {
              this.erFn(res.data.msg)
            }
          }).catch((error) => {
            this.erFn(error);
          })
        }).catch(() => {
          this.$message({
            type: 'info',
            message: 'Canceled deletion'
          });
        });
      },
      // 新增数据
      addData() {
        this.$http.post('', this.form).then((res) => {
          if (res.data.status === 200) {
            this.suFn(res.data.msg)
            this.showDialog = false
            this.listPage()
          } else {
            this.erFn(res.data.msg)
          }
        }).catch((error) => {
          this.erFn(error);
        })
      },
      // 修改数据
      updateData() {
        this.$http.post('', this.form).then((res) => {
          if (res.data.status === 200) {
            this.suFn(res.data.msg)
            this.showDialog = false
            this.listPage()
          } else {
            this.erFn(res.data.msg)
          }
        }).catch((error) => {
          this.erFn(error);
        })
      },
      // 提交弹窗的表格
      saveDialog(name) {
        /* eslint-disable */
        this.showSaveBtn = true
        this.$refs.forms.validate((valid) => {
          if (valid) {
            switch (title) {
              case 'Add':
                this.addData()
                break;
              case 'Edit':
                this.updateData()
                break;
            }
          } else {
            this.waFn('Please fill in the required items.')
            return false;
          }
        });
        setTimeout(() => {
          this.showSaveBtn = false
        }, 1500)
        /* eslint-disable */
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
      // 关闭弹窗
      closeDialog() {
        this.form = this.$options.data().form
        this.$refs.forms.resetFields();
      },
      // 状态改变
      changeSwitch(event,row) {
        this.$http.get('/rule/focusPaxRule/updateByStatus', {
          params: {
            id: row.id,
            status: event,
            version: row.version
          }
        }).then((res) => {
          if (res.data.status === 200) {
            this.suFn(res.data.msg)
            this.listPage()
          } else {
            this.erFn(res.data.msg)
          }
        }).catch((error) => {
          this.erFn(error);
        })
      },
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
