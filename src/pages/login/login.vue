<template>
  <view class="login">
    <img class="logo" src="@/static/images/logo@2x.png" alt />
    <text class="title">蘑菇在线</text>
    <view>
      <img class="tips" src="@/static/images/login_tips@2x.png" alt />
    </view>
    <button
      class="btn_login"
      open-type="getUserInfo"
      plain
      hover-class="none"
      @getuserinfo="wxlogin"
    >
      <img src="@/static/images/wx_login@2x.png" alt />
    </button>
    <button class="phone_login" hover-class="none" plain @click="toPhoneLogin">手机号登录</button>
    <text class="bottom_tips">Copyright@2020蘑菇在线</text>
  </view>
</template>

<script>
export default {
  methods: {
    // 使用微信登录
    wxlogin() {
      uni.login({
        provider: "weixin",
        success: function(res) {
          console.log(res);
          uni.setStorageSync("code", res.code);
          uni.showToast({
            title: "正在登录...",
            icon: "loading",
            duration: 2000
          });
          setTimeout(() => {
            uni.switchTab({
              url: "/pages/home/home"
            });
          }, 1000);
        }
      });
    },

    // 跳转至手机号登录
    toPhoneLogin() {
      uni.navigateTo({
        url: "/pages/phone-login/phone-login"
      });
    }
  },

  // 打开小程序检查是否已登录, 是则跳转至首页
  onShow() {
    if (uni.getStorageSync("code")) {
      uni.switchTab({
        url: "/pages/home/home"
      });
    }
  }
};
</script>

<style lang="less">
.login {
  display: flex;
  flex-direction: column;
  align-items: center;

  .logo {
    width: 200rpx;
    height: 200rpx;
    margin-top: 150rpx;
  }

  .title {
    font-size: 54rpx;
    line-height: 120rpx;
  }

  .tips {
    width: 270rpx;
    height: 32rpx;
  }

  .btn_login {
    margin-top: 200rpx;
    width: 568rpx;
    height: 98rpx;
    padding: 0;
    border: none;

    img {
      width: 100%;
      height: 100%;
    }
  }

  .phone_login {
    font-size: 32rpx;
    margin-top: 40rpx;
    border: none;
  }

  .bottom_tips {
    position: absolute;
    font-size: 22rpx;
    color: #999;
    bottom: 40rpx;
  }
}
</style>