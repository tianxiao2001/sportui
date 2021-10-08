<template>
    <div class="login_container">
        <!-- 登陆块 -->
        <div class="login_box">
            <!-- 头像 -->
        <div class="avatar_box">
            <img src="../assets/th.png" class="img1" alt/>
        </div>
        <!-- 表单区域 -->
        <el-form ref="loginFormRef" :rules="loginRules" :model="loginForm" class="login_form" label-width="0">
          <!-- 用户名 -->
          <el-form-item prop="username">
          <el-input el-input v-model="loginForm.username" prefix-icon="iconfont icon-denglu-copy"></el-input>
          </el-form-item>
          <!-- 密码 -->
          <el-form-item prop="password">
          <el-input v-model="loginForm.password" prefix-icon="iconfont icon-mima" show-password></el-input>
          </el-form-item>
          <!-- 按钮 -->
          <el-form-item class="btns">
          <el-button type="primary" @click="login()">登录</el-button>
          <el-button type="info" @click="resetLoginForm()" >重置</el-button>
          </el-form-item>
        </el-form>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return{
            // 表单数据
            loginForm:{
                username:"tianxiao",
                password:"200153"
            },
            // 验证对象
            loginRules:{
                username:[
                    { required: true, message: '请输入用户名称', trigger: 'blur' },//必填项验证
                    { min: 3, max: 8, message: '长度在 3 到 8 个字符', trigger: 'blur' }//必填项验证
                ],
                password:[
                     { required: true, message: '请输入用户密码', trigger: 'blur' },//必填项验证
                    { min: 6, max: 8, message: '长度在 6 到 8 个字符', trigger: 'blur' }//必填项验证
                ],
            },
        };
    },   
    methods:{
        // 重置表单内容
        resetLoginForm(){
            this.$refs.loginFormRef.resetFields();
        },
        login(){
            this.$refs.loginFormRef.validate(async valid =>{
                if(!valid) return;
                const{data:res}=await this.$http.post("login",this.loginForm);//访问后台
                if(res.flag=="ok"){
                    window.sessionStorage.setItem("user",res.user);//存储user对象
                    this.$message.success("操作成功！！！");
                    this.$router.push({path:"/home"});
                }else{
                    this.$message.error("操作失败！！！");
                }
            })
        },
    },
}
// 根节点样式
</script>
<style scoped>
.login_container{
    background-color: #2b4b6b;
    height: 100vh;
}
.login_box{
    width: 450px;
    height: 300px;
    background-color: #fff;
    border-radius: 5px;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50px);
}
.avatar_box{
        width: 130px;
        height: 130px;
        border:1px solid #eee;
        border-radius:75%;
        padding: 1px;
        box-shadow: 0 0 10px #ddd;
        position: absolute;
        left: 50%;
        transform: translate(-50%,-50px);
        background-color: #0ee;
    }
    .img1{
        width: 130px;
        height: 130px;
        border-radius: 75%;
        background-color: #eee;
    }
    .btns{
        display: flex;
        justify-content: flex-end;
    }
    .login_form{
        position: absolute;
        bottom: 0px;
        width: 100%;
        padding: 0 10px;
        box-sizing: border-box;
    }
    .btns{
        display: flex; 
        justify-content: center;
    }

</style>