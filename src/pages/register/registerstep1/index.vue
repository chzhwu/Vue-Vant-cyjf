<template>
  <div class="register">
    <div class="step">
      <span class="cir active"></span>
      <span class="line"></span>
      <span class="cir"></span>
      <span class="line"></span>
      <span class="cir"></span>
    </div>
    <div class="content1">
      <div class="ipt">
        <input type="text" v-model="mobile" placeholder="请输入手机号码" maxlength="16">
      </div>
      <router-link class="mid frt" to="/login">
        我有账号，立即登录
      </router-link>
      <!-- <router-link class="btn" :to="{path:'/registerstep2',query:{mobile:mobile}}">
        <button>下一步</button>
      </router-link> -->
      <div class="btn">
        <button @click="next">下一步</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "register",
  components: {},
  props: [],
  data() {
    return {
      active: 0,
      mobile: ""
    };
  },
  created() {},
  mounted() {},
  methods: {
    next() {
      let isPhone = this.$util.isPhone(this.mobile);
      if (this.mobile == "") {
        this.$toast("请输入手机号");
        return;
      } else if (!isPhone) {
        this.$toast("请输入正确的手机号");
        return;
      } else {
        this.axios
          .post(`regist/checkMobile?mobile=${this.mobile}&type=${"GENERAL"}`)
          .then(res => {
            if (res.success) {
              this.$router.push({
                name: "registerstep2",
                query: { mobile: this.mobile }
              });
            } else {
              this.$toast(res.message);
            }
          })
          .catch(err => {});
      }
    }
  }
};
</script>

<style scoped lang="scss">
.register {
  .code {
    width: 30%;
    height: 51px;
    line-height: 51px;
    text-align: center;
    font-size: 16px;
    text-decoration: none;
    outline-style: none;
    color: #ff9800;
    border: 1px solid #ff9800;
    border-radius: 5px;
  }
  .btn {
    width: 100%;
    height: 46px;
    margin-top: 15px;
    button {
      width: 100%;
      color: #fff;
      background-color: #ff9800;
      font-size: 18px;
      line-height: 46px;
      border-style: none;
      border-radius: 5px;
    }
  }
  .step {
    height: 57px;
    background-color: #fff;
    padding: 20px 60px;
    box-sizing: border-box;
    .cir {
      float: left;
      width: 15px;
      height: 15px;
      border: 1px solid #6980f5;
      background-color: #fff;
      border-radius: 50%;
    }
    .cir.active {
      background-color: #6980f5;
    }
    .line {
      float: left;
      width: 100px;
      height: 1px;
      background-color: #6980f5;
      margin: 8px 0;
    }
  }
  .content1 {
    padding: 0 23px 23px 23px;
    background-color: #fff;
    .ipt {
      width: 100%;
      height: 50px;
      input {
        width: 100%;
        height: 100%;
        font-size: 16px;
        text-indent: 4px;
        border-bottom: 1px solid #ccc;
      }
    }
  }
  .content1 .mid {
    height: 45px;
    color: #879aff;
    font-size: 14px;
    line-height: 45px;
  }
}
</style>