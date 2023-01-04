<template>
  <div class="login">
    <el-form ref="form" :model="form" :rules="rules" class="login_form" @submit.native="register">
      <!--<h1 class="system_title">在线网盘游客登录</h1>-->
     <div>
       <img :src="src/imgs/viewer.png">
     </div>
      <el-row class="mb-4">
        <el-button type="primary" plain><font style="color: white">游客登录</font></el-button>
      </el-row>

    </el-form>
  </div>
</template>

<script>
export default {
  name: "index",
  methods: {
    viewer(e) {
      e.preventDefault();
      this.$refs.form.validate((val) => {
        if (val) {
          const params = {
            email: this.form.email,
            word: md5(this.form.word),
          };
          this.$api.viewaer(params).then((res) => {
            // console.log(res);
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

<style scoped>
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
</style>
