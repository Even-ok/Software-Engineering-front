<template>
  <el-container style="margin-top:20px;">
    <el-main>
      <el-card
        style="
          box-shadow: 7px 7px 7px rgba(0, 0, 0, 0.15);
          margin-left: 15%;
          margin-right: 15%;
        "
      >
        <el-form
          ref="userAccount"
          style="margin: 40px 100px 0px 50px"
          :model="form"
          label-width="80px"
        >
          <el-form-item label="原密码" :required="true" status-icon="true">
            <el-input type="password" v-model="form.oripassword"></el-input>
          </el-form-item>

          <el-form-item label="新密码" :required="true" status-icon="true">
            <el-input type="password" v-model="form.password"></el-input>
          </el-form-item>

          <el-form-item label="再次输入" :required="true" status-icon="true">
            <el-input type="password" v-model="form.passwordC"></el-input>
          </el-form-item>

          <el-form-item
            label="邮箱"
            :required="true"
            prop="email"
            status-icon="true"
          >
            <el-input v-model="form.email"></el-input>
          </el-form-item>

          <el-form-item label="验证码" :required="true" status-icon="true">
            <el-input type="text" v-model="form.captcha"></el-input>
          </el-form-item>

          <el-form-item  :required="true" status-icon="true">
            <el-button type="text" >发送验证码</el-button>
          </el-form-item>

          <el-form-item>
            <el-button style="margin-left: 30%" @click="validateCaptcha()" type="primary"
              >确认修改</el-button
            >
          </el-form-item>
        </el-form>
      </el-card>
    </el-main>
  </el-container>
</template>

<script>
export default {
  data() {
    return {
      form: {
        password: "",
        passwordC: "",
        oripassword:"",
        captcha:"",
        captchaSuccess:"false",
      },
    };
  },
  methods: {
      validateCaptcha(){
        this.form.captchaSuccess = "false";
        //var result = [];
      },

    back() {
      this.$router.push("/studentHome");
    },
  },
};
</script>
