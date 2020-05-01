<template>
  <div class="phone-login">
    <p class="title">手机号验证</p>
    <p class="subTitle">用于即时获取课程最新信息</p>
    <div class="phone">
      <input type="tel" v-model="phone" placeholder="请输入您的手机号" />
      <div class="btn_code" :class="{'countDown':count}" @click="getVcode">{{tip}}</div>
    </div>
    <div class="vcode">
      <input type="number" v-model="vcode" placeholder="请输入验证码" maxlength="4" />
    </div>
    <button plain hover-class="none" class="btn_check" @click="chenkVcode">
      <img src="@/static/images/phone_login@2x.png" alt />
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      phone: null,
      vcode: null,
      tip: "获取验证码",
      count: 0
    };
  },
  methods: {
    // 获取验证码的方法
    getVcode() {
      // 是否在倒计时中
      if (this.count !== 0) return;

      // 验证手机号格式
      if (!/^1[34578]\d{9}$/.test(this.phone)) {
        uni.showToast({
          title: "手机号格式错误!",
          duration: 2000,
          icon: "none"
        });
        return;
      }

      // 发送请求获取验证码, 进入倒计时
      setTimeout(() => {
        uni.showToast({
          title: "2233",
          duration: 2000,
          icon: "none"
        });
      }, 2000);
      this.count = 10;
      this.tip = this.count + "s";
      let timer = setInterval(() => {
        this.count--;
        if (this.count === 0) {
          this.tip = "获取验证码";
          clearInterval(timer);
          return;
        }
        this.tip = this.count + "s";
      }, 1000);
    },

    // 验证手机验证码并登录
    chenkVcode() {
      if (!this.vcode || this.vcode.toString().length !== 4) {
        uni.showToast({
          title: "请输入短信验证码!",
          duration: 2000,
          icon: "none"
        });
        return;
      }

      if (this.vcode == 2233) {
        uni.showLoading({
          title: "登陆中..."
        });
        setTimeout(() => {
          uni.hideLoading();
          uni.switchTab({
            url: "/pages/home/home"
          });
        }, 1000);
      } else {
        uni.showToast({
          title: "验证码错误",
          duration: 2000,
          icon: "none"
        });
      }
    }
  }
};
</script>

<style lang="less" scoped>
.phone-login {
  padding: 0 60rpx;
  .title {
    font-size: 44px;
    line-height: 180rpx;
  }
  .subTitle {
    font-size: 14px;
    line-height: 40rpx;
    color: #999;
  }
  .phone {
    display: flex;
    width: 100%;
    height: 80rpx;
    border-bottom: 1px solid #e9e9e9;
    margin-top: 150rpx;

    input {
      flex: 1;
      height: 100%;
    }

    .btn_code {
      width: 170rpx;
      height: 60rpx;
      font-size: 12px;
      border: 2rpx solid #a8a8a8;
      border-radius: 30rpx;
      line-height: 60rpx;
      text-align: center;
    }

    .countDown {
      color: #999;
    }
  }

  .vcode {
    width: 100%;
    height: 80rpx;
    border-bottom: 1px solid #e9e9e9;
    margin-top: 90rpx;

    input {
      height: 100%;
    }
  }

  .btn_check {
    width: 100%;
    height: 100rpx;
    margin: 280rpx auto 0;
    border: none;

    img {
      width: 100%;
      height: 100%;
    }
  }
}
</style>