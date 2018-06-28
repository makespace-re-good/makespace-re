<template id="teacherManager">
  <div align="right">
    <div id="manage">
      <!--标题-->
      <div align="left"><label id="tabelName">导师管理</label></div>
      <div align="right"><el-button @click.native.prevent="addHandle" type="primary"  plain>新增</el-button></div>
      <br/>
      <!--显示信息表-->
      <el-table  :data="teacher" stripe  style="width: 100%" max-height="250">
        <el-table-column prop="name" label="姓名" width="100"></el-table-column>
        <el-table-column prop="title" label="职称" width="80"></el-table-column>
        <el-table-column prop="phone" label="电话" width="180"></el-table-column>
        <el-table-column prop="email" label="邮箱" width="200"></el-table-column>
        <el-table-column label="操作">
          <template slot-scope="scope">
            <div>
              <el-button @click.native.prevent="updateHandle(scope.$index, teacher)" type="success" icon="el-icon-edit" circle></el-button>
              <el-button @click.native.prevent="deleteRow(scope.$index, teacher)" type="danger" icon="el-icon-delete" circle></el-button>
            </div>
          </template>
        </el-table-column>
      </el-table>
    </div>
    <div align="left">
      <!--修改表单页面-->
      <el-dialog :visible.sync="updateVisible" :close-on-click-modal="false"  :show-close="false" title="修改导师信息" @open="openCheck()">
        <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm" >
          <el-form-item label="姓名" prop="name" :label-width="formLabelWidth">
            <el-input v-model="ruleForm.name" auto-complete="off" ></el-input>
          </el-form-item>
          <el-form-item label="职称" prop="title" :label-width="formLabelWidth" required="">
            <el-select v-model="ruleForm.title" placeholder="请选择您的职称">
              <el-option label="教授" value="教授"></el-option>
              <el-option label="副教授" value="副教授"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="电话" prop="phone" :label-width="formLabelWidth">
            <el-input v-model="ruleForm.phone" auto-complete="off"></el-input>
          </el-form-item>
          <el-form-item label="邮箱" prop="email" :label-width="formLabelWidth">
            <el-input v-model="ruleForm.email" auto-complete="off"></el-input>
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button type="primary" @click="submitUpdate('ruleForm')">提交修改</el-button>
          <el-button @click="resetUpdateForm('ruleForm')">取 消</el-button>
        </div>
      </el-dialog>
    </div>

    <div align="left">
      <!--创建表单页面-->
      <el-dialog :visible.sync="addVisible" :close-on-click-modal="false" :show-close="false" title="新增导师信息" >
        <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
          <el-form-item label="姓名" prop="name" :label-width="formLabelWidth">
            <el-input v-model="ruleForm.name" auto-complete="off" placeholder="请输入姓名"></el-input>
          </el-form-item>
          <el-form-item label="职称" prop="title" :label-width="formLabelWidth">
            <el-select v-model="ruleForm.title" placeholder="请选择您的职称">
              <el-option label="教授" value="教授"></el-option>
              <el-option label="副教授" value="副教授"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="电话" prop="phone" :label-width="formLabelWidth">
            <el-input v-model="ruleForm.phone" auto-complete="off" placeholder="请输入您的电话"></el-input>
          </el-form-item>
          <el-form-item label="邮箱" prop="email" :label-width="formLabelWidth">
            <el-input v-model="ruleForm.email" auto-complete="off" placeholder="请输入您的邮箱"></el-input>
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button id="create" type="primary" @click="submitForm('ruleForm')">立即创建</el-button>
          <el-button @click="resetAddForm('ruleForm')">取 消</el-button>
        </div>
      </el-dialog>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        teacher: [{                                  //记录教师信息数组
          name: '老师名',
          title : '教授',
          phone:'13512312314',
          email: 'w.asd@xmu.edu'
        }],
        ruleForm: {                                    //表单项
          name: '',
          title: '教授',
          phone: '',
          email: '',
          index:''
        },
        flagname:false,
        flagphone:false,
        flagemail:false,
        rules:{                                        //rules
          name:[
            { validator:(rule,value,callback)=>{                      //姓名验证
                if(/^[\u4e00-\u9fa5A-Za-z0-9-_]{1,}$/.test(value) == false){
                  callback(new Error("请输入姓名"));
                  this.$data.flagname=false;
                }else{
                  this.$data.flagname=true;
                  callback();
                }
              },required: true, trigger: '' },
          ],
          title:[
            {required: true, trigger: 'change' }
          ],
          phone:[
            { validator:(rule,value,callback)=>{                      //电话验证
                if(/^(((13[0-9]{1})|(15[0-9]{1})|(18[0-9]{1}))+\d{8})$/.test(value) == false){
                  this.$data.flagphone=false;
                  callback(new Error("请输入有效电话"));
                }else{
                  this.$data.flagphone=true;
                  callback();
                }
              },required: true, trigger: 'blur' },
          ],
          email:[
            {
              validator:(rule,value,callback)=>{                     //邮箱验证
                if(/[a-z0-9]+([._\\-]*[a-z0-9])*@([a-z0-9]+[-a-z0-9]*[a-z0-9]+.){1,63}[a-z0-9]+$/.test(value) == false){
                  callback(new Error("请输入有效邮箱"));
                  this.$data.flagemail=false;
                }else{
                  this.$data.flagemail=true;
                  callback();
                }
              },required: true, trigger: 'blur' }
          ],
        },
        formLabelWidth: '120px',
        updateVisible:false,
        addVisible:false,
      }
    },
    methods:{
      openCheck(){                                         //打开修改界面时调用
        this.$data.ruleForm.name=this.$data.teacher[this.$data.ruleForm.index].name;
        this.$data.ruleForm.title=this.$data.teacher[this.$data.ruleForm.index].title;
        this.$data.ruleForm.phone=this.$data.teacher[this.$data.ruleForm.index].phone;
        this.$data.ruleForm.email=this.$data.teacher[this.$data.ruleForm.index].email;
        this.$data.flagemail=true;
        this.$data.flagphone=true;
        this.$data.flagname=true;
      },
      updateHandle(index, rows) {                              //弹出修改界面
        this.updateVisible=true
        this.$data.ruleForm.index=index;
      },
      addHandle(){                                           //弹出添加界面
        this.addVisible=true;
        this.$data.flagemail=false;
        this.$data.flagphone=false;
        this.$data.flagname=false;
        this.$data.ruleForm.name='';
        this.$data.ruleForm.title='教授';
        this.$data.ruleForm.phone='';
        this.$data.ruleForm.email='';
      },
      submitForm(formName) {                                 //创建项目提交
        if (this.$data.flagphone === false || this.$data.flagemail === false || this.$data.flagname === false) {
          this.$notify.error({
            title: '错误',
            message: '创建输入无效，请修正输入'
          });
        }
        else {
          this.$data.teacher.push(
            {
              name: this.$data.ruleForm.name,
              title: this.$data.ruleForm.title,
              phone: this.$data.ruleForm.phone,
              email: this.$data.ruleForm.email
            });
          this.$data.addVisible = false;
          this.$data.flagname=false;
          this.$data.flagphone=false;
          this.$data.flagemail=false;
          this.$refs[formName].resetFields();
        }
      },
      submitUpdate(formName){                                      //提交修改
        if(this.$data.flagphone===false||this.$data.flagemail===false||this.$data.flagname===false)
          this.$notify.error({
            title: '错误',
            message: '修改无效，请修正输入'
          });
        else {
          this.$data.teacher[this.$data.ruleForm.index].name = this.$data.ruleForm.name;
          this.$data.teacher[this.$data.ruleForm.index].title = this.$data.ruleForm.title;
          this.$data.teacher[this.$data.ruleForm.index].phone = this.$data.ruleForm.phone;
          this.$data.teacher[this.$data.ruleForm.index].email = this.$data.ruleForm.email;

          this.$data.flagname=false;
          this.$data.flagphone=false;
          this.$data.flagemail=false;
          this.$data.updateVisible = false;
          this.$refs[formName].resetFields();
        }
      },
      resetUpdateForm(formName){                                 //退出修改界面，重置ruleForm
        this.$data.updateVisible=false;
        this.$data.flagname=false;
        this.$data.flagphone=false;
        this.$data.flagemail=false;
        this.$refs[formName].resetFields();
      },
      resetAddForm(formName){                                   //退出创建界面，重置ruleForm
        this.$data.addVisible=false;
        this.$data.flagname=false;
        this.$data.flagphone=false;
        this.$data.flagemail=false;
        this.$refs[formName].resetFields();
      },
      deleteRow(index, rows) {                          //删除该记录
        this.$confirm('此操作将永久删除该条记录, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          rows.splice(index, 1);
          this.$message({
            type: 'success',
            message: '删除成功!'
          });
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          });
        });
      },
    }
  }
</script>

<style scoped>
  #manage{
    width:85%;
  }
  #tabelName{
    font-size: 45px;
    color: #409ef1 ;
  }
</style>
