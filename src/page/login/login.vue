<template>
  <div class="admin-login-box">
    <!--后台的登录路口,只有登录,没有注册,也没有找回密码-->
    <!--只有门户一个用户入口,如果是管理员则跳转到管理中心,否则跳转到首页/重定向的页面-->
    <!--如果是门户的登录,则有登录、注册、找回密码这些功能-->
    <!--顶部内容-->
    <div class="admin-login-header-box">
      <div class="admin-login-header-center center">
        <div class="admin-login-logo">
          博客系统|登录
        </div>
      </div>
    </div>
    <!--中间内容-->
    <div class="admin-login-content-box">
      <div class="admin-login-content-center center">
        <el-form
            label-position="left"
            label-width="100px"
            style="max-width: 400px"
            v-model="loginInfo">
          <el-form-item label="账号:">
            <el-input v-model="blogUser.userName"/>
          </el-form-item>
          <el-form-item label="密码:">
            <el-input v-model="blogUser.password"/>
          </el-form-item>
          <el-form-item label="人类验证码:">
            <el-row>
              <el-col :span="12">
                <el-input v-model="loginInfo.verifyCode"/>
              </el-col>
              <el-col :span="12">
                <img :src="loginInfo.captchaPath" alt="" @click="updateVerifyCode"/>
              </el-col>
            </el-row>
          </el-form-item>
          <el-form-item style="background: none;border: none;margin-left:15px ">
            <el-button type="primary" plain> 登 录</el-button>
          </el-form-item>
        </el-form>
      </div>
    </div>
    <!--底部内容-->
  </div>
</template>
<script>
import {reactive, onMounted} from "vue";

const axios = require('axios')
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "login",
  setup() {
    const blogUser = reactive({
      userName: "",
      password: ""
    })
    const loginInfo = reactive({
      from: "",
      captchaPath: "",
      captchaKey: "",
      verifyCode: ""
    })

    const updateVerifyCode = () => {
      loginInfo.captchaPath = "https://api.sunofbeaches.com/uc/ut/captcha?code=" + loginInfo.captchaKey + "&random=" + Date.parse(new Date());
    }

    const doLogin = () => {
      //发起登录

      //TODO:检查数据

      //TODO
      axios({
        method:'post'
      })
    }

    onMounted(() => {
      axios.get('https://api.sunofbeaches.com/shop/discovery/categories')
          .then(res => {
            console.log(res)
          })
      loginInfo.captchaKey = Date.parse(new Date())
      updateVerifyCode();
    })

    return {
      blogUser,
      loginInfo,
      updateVerifyCode
    }
  }
}
</script>

<style lang="less" scoped>

.admin-login-header-box {
  width: 100%;
  height: 46px;
  background: dodgerblue;
}

.admin-login-logo {
  color: #ffffff;
}

.center {
  margin: 0 auto;
  width: 1140px;
}

.admin-login-header-center {
  line-height: 46px;
}

.admin-login-content-box {
  width: 100%;
  background: #ffffff;
  margin: 25px 0;
}

.admin-login-content-center {
  height: 300px;
  border-radius: 5px;
  box-shadow: 0 1px 10px #afafafaf;
  display: flex;
  align-items: center;
}


.el-form-item {
  background: #e6e6e6;
  border: solid 1px #e6e6e6;
  border-radius: 5px;
  text-align: center;
  margin-left: 20px;
}

/deep/ .el-form-item .el-form-item__label {
  display: block;
  padding: 0 0 0 0;
}

.el-row {
  align-items: center;
}

img {
  height: 30px;
  width: 100%;
  //margin: 1px 1px 1px 1px;
  border-radius: 4px;
  display: flex;
}

</style>