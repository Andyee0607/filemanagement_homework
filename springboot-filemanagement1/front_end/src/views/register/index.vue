<template>
  <div class="login">
    <el-form ref="form" :model="form" :rules="rules" class="login_form" @submit.native="register">
      <!--<h1 class="system_title">在线网盘验证登录</h1>-->
      <el-form-item label="邮箱" prop="email">
        <el-input class="login_form_input" v-model="form.email" :autofocus="true"></el-input>
      </el-form-item>
      <el-form-item label="验证码" prop="word">
        <el-input class="login_form_input" v-model="form.word"></el-input>
      </el-form-item>
      <el-row class="mb-4">
        <el-button type="primary" plain><font style="color: #409EFF">获取验证码</font></el-button>
      </el-row>
      <el-form-item class="login_form_button">
        <el-button native-type="submit" type="primary">登录</el-button>
      </el-form-item>
      <div class="mb-2 flex items-center text-sm">
        <el-radio-group v-model="text" class="ml-4">
          <el-radio label="1-8" size="1">未注册邮箱登陆时会自动创建账号，我已阅读并同意
            <font style="color: #409EFF">服务协议</font>和<font style="color: #409EFF">隐私权条款</font></el-radio>
        </el-radio-group>
      </div>
    </el-form>
  </div>
</template>
<script>
  import md5 from 'blueimp-md5';
  import eventBus from '@/libs/event-bus';
  export default {
    name: 'login',
    data() {
      return {
        form: {
          email: '',
          word: ''
        },
        rules: {
          email: [
            { required: true, message: '请输入邮箱', trigger: 'blur' },
            { pattern: /^.{1,100}$/, message: '用户名过长该邮箱已注册', trigger: 'blur' },
          ],
          word: [
            { required: true, message: '请输验证码', trigger: 'blur' }
          ]
        }
      }
    },
    methods: {
      register(e) {
        e.preventDefault();
        this.$refs.form.validate((val) => {
          if (val) {
            const params = {
              email: this.form.email,
              word: md5(this.form.word),
            };
            this.$api.register(params).then((res) => {
              // console.log(res);
              window.localStorage.setItem('email', this.form.name);
              window.localStorage.setItem('token', res.data.token);
              window.localStorage.setItem('admin', res.data.admin);
              eventBus.$emit('LOGIN');
              this.$router.push({ path: '/main' });
            });
          }
        });
      },
    }
  }
</script>

<style lang="scss" scoped>
  .login{
    position: relative;
    height: 100%;
    width: 100%;
    /*background-image: url("../../assets/imgs/login_bg.jpg");*/
    background-image: linear-gradient(45deg, #ddd, #00dbde);
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center center;
  }
  .login_form{
    position: absolute;
    top: 40%;
    left: 50%;
    transform: translate(-50%, -50%);
    /*border: 1px solid #ddd;*/
    border-radius: 6px;
    width: 416px;
    padding: 20px;
    background-color: rgba(255, 255, 255, 0.2);
    max-width: 80%;
  }
  .login_form_button{
    text-align: center;
  }
  .login_form_input{
    input{
      background-color: transparent;
    }
  }
  .system_title{
    text-align: center;
    color: #606266;
    margin-bottom: 20px;
    font-size: 26px;
  }
  .registered{
    margin-top: 10px;
    a{
      color: #606266;
      text-decoration: underline;
    }
  }
</style>
