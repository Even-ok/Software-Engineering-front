<template>
  <div style="margin: auto auto; height: 620px">
    <div style="height: 620px">
      <el-container class="loginPage" style="mardin-top: 0px">
        <el-main
          style="
            padding: 0px;
            filter: brightness(85%);
            width: 100%;
            overflow: hidden;
          "
        >
          <img
            src="@/assets/home_left.jpg"
            style="height: 560px; overflow: hidden"
          />
        </el-main>

        <el-aside width="500px" class="loginForm" style="height: 560px">
          <el-container>
            <el-header height="150px">
              <p
                style="
                  margin: 70px auto 50px auto;
                  color: white;
                  font: 32px Microsoft YaHei;
                "
              >
                实验教学系统
              </p>
            </el-header>
            <el-main class="login_back" style="padding: 0px">
              <el-form
                ref="ruleForm"
                :model="ruleForm"
                status-icon
                :rules="rules"
                label-width="80px"
              >
                <!-- <el-form-item label="您的身份" prop="role">
                  <el-select class="select" v-model="role" placeholder="请选择">
                    <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
                    </el-option>
                  </el-select>
                </el-form-item> -->
                <el-form-item label="用户名" prop="id">
                  <el-input
                    v-model="ruleForm.id"
                    type="text"
                    autocomplete="off"
                    placeholder="请输入学号/工号/账号"
                  ></el-input>
                </el-form-item>
                <el-form-item label="密码" prop="password">
                  <el-input
                    v-model="ruleForm.password"
                    type="password"
                    autocomplete="off"
                    placeholder="请输入密码"
                  >
                  </el-input>
                </el-form-item>
                <el-form-item>
                  <el-button type="primary" @click="submitForm()"
                    >登陆</el-button
                  >
                  <el-button @click="openMask" style="margin-left: 10%"
                    >忘记密码</el-button
                  >

                  <br />
                  <br />

                  <br />
                  <el-form-item>
                    <dialog-bar
                      v-model="sendVal"
                      type="danger"
                      title="忘记密码"
                      content="忘记密码"
                      v-on:cancel="clickCancel()"
                      @danger="clickDanger()"
                      @confirm="clickConfirm()"
                      dangerText="提交"
                    ></dialog-bar>
                  </el-form-item>
                </el-form-item>
              </el-form>
            </el-main>
          </el-container>
        </el-aside>
      </el-container>
    </div>
    <div class="outFunction">
      <h2>系 统 功 能</h2>
      <el-container height="400px" style="padding-top: 30px">
        <el-col
          :span="4"
          v-for="(item, index) in main_title"
          :key="index"
          class="system_pic"
          :offset="index > 0 ? 1 : 0"
        >
          <el-card style="box-shadow: 7px 7px 7px rgba(0, 0, 0, 0.15)">
            <img :src="item.img" class="img" />
            <div style="padding: 14px">
              <p class="text" style="text-transform: uppercase !important">
                {{ item.title }}
              </p>
            </div>
          </el-card>
        </el-col>
      </el-container>
    </div>

    <div class="ExperimentIntro" style="padding-top: 50px; margin-bottom: 30px">
      <h2>实 验 介 绍</h2>
      <p style="padding-top: 10px">
        本系统中包含多个在线模拟的实验项目，如不确定性分析实验、拍卖实验、盈亏平衡实验、经济寿命周期实验等。学生可通过本系统进行线上实验，帮助线下教学理解。
      </p>

      <el-carousel
        :interval="4000"
        type="card"
        height="500px"
        style="padding-left: 50px; padding-right: 50px; padding-top: 25px"
      >
        <el-carousel-item v-for="item in imageList" :key="item.id">
          <img :src="item.su" />
        </el-carousel-item>
      </el-carousel>
    </div>
    <div
      class="contact"
      id="contact"
      style="height: 160px; background: #99ccff"
    >
      <el-col
        :span="4"
        v-for="index of 4"
        :key="index"
        class="us"
        :offset="index > 0 ? 2 : 1"
        style="margin-top: 30px"
      >
        <h4 class="text-uppercase">Contact us</h4>
        <p class="address">
          Tongji University <br />
          Shanghai, <br />
          201800
        </p>
      </el-col>
    </div>
  </div>
</template>



<script>
import axios from "axios";
// import courseScoreVue from "../teacher/course/courseDetail/courseScore.vue";
import dialogBar from "./dialog.vue";
export default {
  components: {
    "dialog-bar": dialogBar,
  },
  data() {
    const validatePass = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入学号"));
      } else {
        if (this.ruleForm.id !== "") {
          this.$refs.ruleForm.validateField("checkPass");
        }
        callback();
      }
    };
    const validatePass2 = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入密码"));
      } else {
        callback();
      }
    };
    return {
      imageList: [
        {
          id: 0,
          su: require("../../assets/2.jpg"),
        },

        {
          id: 1,
          su: require("../../assets/3.jpg"),
        },
        {
          id: 2,
          su: require("../../assets/4.jpg"),
        },
      ],

      ruleForm: {
        id: "10001",
        password: "123",
      },
      rules: {
        id: [{ validator: validatePass }],
        password: [{ validator: validatePass2 }],
      },
      options: [
        {
          value: "student",
          label: "学生",
        },
        {
          value: "teacher",
          label: "老师",
        },
        {
          value: "teachingAssistant",
          label: "助教",
        },
        {
          value: "admin",
          label: "管理员",
        },
      ],
      main_title: [
        {
          img: require("@/assets/user_manage.jpeg"),

          title: "用户管理",
          text: 10,
        },
        {
          img: require("@/assets/teaching.jpeg"),
          title: "实验教学",
          text: 5,
        },
        {
          img: require("@/assets/Analysis.png"),
          title: "实验分析",
          text: 20,
        },
        {
          img: require("@/assets/pk.jpeg"),
          title: "对抗练习",
          text: 5,
        },
        {
          img: require("@/assets/online_lab.png"),
          title: "在线模拟",
          text: 6,
        },
      ],
      role: "student",
      login_left: "require('@/assets/login_back.jpg')",
      sendVal: false,
    };
  },
  methods: {
    openMask() {
      this.$store.state.data = "";
      this.sendVal = true;
    },

    submitForm() {
      if (this.ruleForm.id === "" && this.ruleForm.password === "") {
        this.$message("账户和密码不能为空！");
      } else if (this.ruleForm.id === "") {
        this.$message("请输入账户！");
      } else if (this.ruleForm.password === "") {
        this.$message("请输入密码！");
      } else {
        //学生登录
        sessionStorage.setItem("id", this.ruleForm.id);
        axios({
          method: "POST",
          baseURL: "/api",
          url: "/user/login",

          data: this.ruleForm,
        })
          .then((res) => {
            if (res.data.code === 200) {
              sessionStorage.setItem("role", 1);
              this.$message({
                message: "登陆成功",
                type: "success",
              });
              // console.log(res);
              sessionStorage.setItem("role", res.data.data.identity);
              sessionStorage.setItem("authorities", res.data.data.authorities);
              sessionStorage.setItem("token", res.data.data.token);
              sessionStorage.setItem("id", res.data.data.userid);
              console.log(res.data.data.identity === 1);
              switch (res.data.data.identity) {
                case "1":
                  console.log("管理员");
                  this.$router.push("/adminHome");
                  break;
                case "2":
                  this.$router.push("/teacherHome/control");
                  break;
                case "3":
                  this.$router.push("/teacherHome/control");
                  break;
                case "4":
                  this.$router.push("/studentHome/control");
                  break;
                case "5":
                  this.$router.push("/studentHome/control");
                  break;
                default:
                  break;
              }
            }
          })
          .catch((err) => {
            console.log(err);
            this.$message({
              message: "服务器错误",
              type: "error",
            });
          });
      }
    },
  },
};
</script>

<style scoped>
body > .el-container {
  margin-bottom: 40px;
}

.loginPage {
  text-align: center;
  line-height: 570px;
}

.loginForm {
  text-align: center;

  line-height: 570px;
  height: 560px;
  padding-right: 30px;
  padding-top: 20px;
  background: rgba(27, 41, 58, 0.85);
}

.text-button {
  color: white;
}

.select {
  width: 330px;
}

.text-button:hover {
  color: #bbdefb;
}

.outFunction {
  margin-top: 30px;
  padding: 20px;
}

.bottom {
  margin-top: 13px;
  line-height: 12px;
}

.button {
  padding: 0;
  float: right;
}

.image {
  width: 100%;
  display: block;
}

.clearfix:before,
.clearfix:after {
  display: table;
  content: "";
}

.clearfix:after {
  clear: both;
}

.el-carousel__item h3 {
  color: #475669;
  font-size: 14px;
  opacity: 0.75;
  line-height: 200px;
  margin: 0;
}

.el-carousel__item:nth-child(2n) {
  background-color: #99a9bf;
}

.el-carousel__item:nth-child(2n + 1) {
  background-color: #d3dce6;
}

.el-button--primary {
  color: white;
}

.el-button--success {
  color: white;
}
</style>