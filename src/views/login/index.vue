<template>
  <div class="login-container">
    <div class="logo" />
    <div class="form">
  <h1>登录</h1>
  <el-card shadow="never" class="login-card">
    <!--登录表单-->
    <!-- el-form > el-form-item > el-input -->
    <el-form :model="list" :rules="rules">
      <el-form-item prop="phone">
        <el-input placeholder="请输入手机号" v-model="list.phone"/>
      </el-form-item>
      <el-form-item prop="password" >
        <el-input placeholder="请输入密码" v-model="list.password"/>
      </el-form-item>
      <el-form-item prop="protocol">
        <el-checkbox v-model="list.protocol"> 
          用户平台使用协议
        </el-checkbox>
      </el-form-item>
      <el-form-item>
        <el-button style="width:350px" type="primary">登录</el-button>
      </el-form-item>
    </el-form>
    </el-card>
  </div>
  </div>
</template>
<script>
export default {
  name : "Login",
  data(){
    //自定义验证手机号
    var checkPhone=(rule, value, callback)=>{
        const phoneReg=/^(?:(?:\+|00)86)?1\d{10}$/
        if (!value) {
          return callback(new Error('年龄不能为空'));
          }else{
          if(phoneReg.test(value)){
            callback()
          }else{
            callback(new Error('手机号格式不正确'))
          }
        }
      }
      //自定义验证用户平台使用协议
      var agreement = (rule, value, callback) => {
        console.log(value);
        value?callback():callback(new Error('您必须勾选用户的使用协议'))
      }
    return{
      list:{
        phone:'',
        password:'',
        protocol:'',
      },
      rules:{
        phone:[ { required: true, message: '请输入手机号', trigger: 'blur' },
      {validator:checkPhone,trigger:'blur'}],
        password:[ { required: true, message: '请输入密码', trigger: 'blur' },
        { min: 6, max: 16, message: '长度在 6 到 16位之间', trigger: 'blur' }],
        protocol:[ { type: 'boolean',required: true, message: '您必须勾选用户的使用协议', trigger: 'change' },
        {validator:agreement,trigger:'change'}]
      },
      
  }
}
}
</script>
<style lang="scss">
.login-container {
  display: flex;
  align-items: stretch;
  height: 100vh;
  .logo {
    flex: 3;
    background: rgba(38, 72, 176) url(../../assets/common/login_back.png)
      no-repeat center / cover;
    border-top-right-radius: 60px;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    justify-content: center;
    padding: 0 100px;
    .icon {
      background: url(../../assets/common/logo.png) no-repeat 70px center /
        contain;
      width: 300px;
      height: 50px;
      margin-bottom: 50px;
    }
    p {
      color: #fff;
      font-size: 18px;
      margin-top: 20px;
      width: 300px;
      text-align: center;
    }
  }
  .form {
    flex: 2;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding-left: 176px;
    .el-card {
      border: none;
      padding: 0;
    }
    h1 {
      padding-left: 20px;
      font-size: 24px;
    }
    .el-input {
      width: 350px;
      height: 44px;
      .el-input__inner {
        background: #f4f5fb;
      }
    }
    .el-checkbox {
      color:#606266;
    }
  }
}
</style>
