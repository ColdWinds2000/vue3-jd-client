<template>
  <div class="login">
    <div class="title">用户注册</div>
    <van-form @submit="onSubmit" label-width="60px">
      <van-cell-group>
        <van-field
          v-model="username"
          name="username"
          label="用户名"
          placeholder="请输入用户名"
          autocomplete="off"
          :rules="[{ validator: checkname }]"
        />
        <van-field
          v-model="password"
          type="password"
          name="password"
          label="密码"
          placeholder="请输入密码"
          :rules="[{ validator: checkpsd }]"
        />
        <van-field
          v-model="repassword"
          type="password"
          name="repassword"
          label="确认密码"
          placeholder="请输入确认密码"
          :rules="[{ validator: checkrepsd }]"
        />
        <van-field
          v-model="phone"
          type="phone"
          name="phone"
          label="手机号"
          placeholder="请输入手机号"
          autocomplete="off"
          :rules="[{ validator: checkphone }]"
        />
      </van-cell-group>
      <div style="margin: 16px 23px">
        <van-button round block type="warning" native-type="submit">
          注册
        </van-button>
      </div>
    </van-form>
    <div class="check">
      <div class="log-phone">
        <router-link to="/mine/logphone">手机号登录</router-link>
      </div>
      <div class="register">
        <router-link to="/mine/login">账号登录</router-link>
      </div>
    </div>
    <div class="else-login">
      <van-divider class="line">其他方式登录</van-divider>
      <div class="icons-login">
        <div class="qq"><van-icon name="qq" /></div>
        <div class="wechat"><van-icon name="wechat" /></div>
        <div class="weibo"><van-icon name="weibo" /></div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
import { Toast } from 'vant'
import { userRegister } from '@/api'
import { checkname, checkphone, checkpsd } from '@/utils/checkinfo'

export default {
  name: 'Register',
  setup() {
    const username = ref('')
    const password = ref('')
    const repassword = ref('')
    const phone = ref('')
    // 用户注册模块
    async function onSubmit(values) {
      userRegister(values)
    }
    const checkrepsd = (val) => {
      let flag = val == password.value
      if (!flag) Toast('两次密码不一致')
      return flag
    }
    return {
      username,
      password,
      repassword,
      phone,
      onSubmit,
      checkname,
      checkphone,
      checkpsd,
      checkrepsd,
    }
  },
}
</script>

<style lang="less" scoped>
.login {
  margin: 5px 20px;
  padding: 10px 0 40px;
  background-color: #fff;
  .title {
    text-align: center;
    padding: 10px 0;
    font-weight: 700;
  }
  .van-button {
    text-indent: 10px;
    letter-spacing: 10px;
  }
  .check {
    padding: 10px 20px 10px 10px;
    display: flex;
    justify-content: space-between;
  }
  .else-login {
    margin: 50px 10px 0;
    .line {
      --van-divider-border-color: #ccc;
    }
    .icons-login {
      display: flex;
      justify-content: center;
      margin: 0 20px;
      > div {
        width: 50px;
        height: 50px;
        font-size: 28px;
        background-color: #e7f7fe;
        border-radius: 50%;
        text-align: center;
        line-height: 50px;
      }
      .qq {
        color: #29bef6;
      }
      .wechat {
        background-color: #e6f8e6;
        margin: 0 30px;
        color: #26c325;
      }
      .weibo {
        color: #ca1e1e;
        background-color: #f2f2f2;
      }
    }
  }
}
</style>
