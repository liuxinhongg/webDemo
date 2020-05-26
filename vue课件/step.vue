<template>
  <div class="box">
    <!-- <about :activenum="2"></about> -->
      <el-steps :active="aa" finish-status="success">
        <el-step title="步骤 1"></el-step>
        <el-step title="步骤 2" ></el-step>
        <el-step title="步骤 3" ></el-step>
    </el-steps>
    <div class="step" v-if='aa==0' >
        <el-form :model="dynamicValidateForm" :rules="emailrules" ref="dynamicValidateForm" label-width="100px" class="demo-dynamic">
            <el-form-item  prop="email" label="邮箱">
                <el-input v-model="dynamicValidateForm.email"></el-input>
            </el-form-item>
            <el-form-item>
                <el-button type="primary" @click="submitemail('dynamicValidateForm')">提交</el-button>
            </el-form-item>
            </el-form>
    </div>
    <div class="step" v-if='aa==1' > 
        <el-form :model="ruleForm" status-icon :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
            <el-form-item label="密码" prop="pass">
                <el-input type="password" v-model="ruleForm.pass" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="确认密码" prop="checkPass">
                <el-input type="password" v-model="ruleForm.checkPass" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item>
                <el-button type="primary" @click="submitForm('ruleForm')">提交</el-button>
                <el-button @click="resetForm('ruleForm')">重置</el-button>
            </el-form-item>
        </el-form>

    </div>
    <div class="step" v-if='aa==2' >
     <!-- <img src="../assets/images/banner.png" alt="" srcset=""> -->
     </div>
    <el-button @click="step">切换</el-button>
    <div :class="num==0 ? class1 : class1active" @mouseover="ys(0)">哈哈哈</div>
    <div :class="num==1 ? class1 : class1active"  @mouseover="ys(1)">发发发</div>
    <div :class="num==2 ? class1 : class1active"  @mouseover="ys(2)">哈哈哈</div>
  </div>
</template>

<script>
import about from './about'
export default {
    data(){
        return{
             aa: 0,
             num:0,
             class1:'boxtext',
             class1active:'boxactive',
             dynamicValidateForm:{
                 email:'',
             },
            ruleForm: {
                pass: '',
                checkPass: '',
            },
            emailrules:{
                 email:[
                    { required: true, message: '请输入邮箱地址', trigger: 'blur' },
                    { type: 'email', message: '请输入正确的邮箱地址', trigger: ['blur', 'change'] }
                ]
            },
            rules:{
                 pass: [{ requred:true, trigger: 'blur',message:'密码不能为空' }],
                checkPass: [{ requred:true, trigger: 'blur',message:'queren密码不能为空' }],
            }
        }
    },
    components:{
        about
    },
    methods: {
        ys(aa){
            this.num=aa;
        },
        step(){
            this.aa++;
        },
        submitemail(formName) {
            this.$refs[formName].validate((valid) => {
                if (valid) {
                    this.$message.success("提交成功");
                    this.step();
                } else {
                    console.log('error submit!!');
                    return false;
                }
            });
        },
        submitForm(formName) {
        // this.$refs[formName].validate((valid) => {
        //   if (valid) {
        //     this.$message.success('提交成功哦')
        //   } else {
        //     console.log('error submit!!');
        //     return false;
        //   }
        // });
        if(this.ruleForm.pass==''){
            this.$message.error('密码不能为空')
        }else if(this.ruleForm.checkPass!=this.ruleForm.pass){
            this.$message.error('确认密码错误')

        }else{
            this.$message.success('提交成功哦')
        }
      },
    },
}
</script>

<style>
.box{
    width: 70%;
    margin: 30px auto;
}
.step{
    width: 80%;
    height: 300px;
    /* background-image: url(../assets/images/banner.png); */
    border: 2px solid red;
    padding: 20px;
    margin: auto;
}
.boxtext{
  color: red;
}
.boxactive{
  color: blue;
  font-weight: bold;
}
</style>
