<template>
  <div class="page-login">
    <div class="logo">
      <img
        src="https://assets.maizuo.com/h5/mz-auth/public/app/img/logo.19ca0be.png"
        alt=""
      />
    </div>
    <div class="login-form">
      <div class="form-group">
        <input
          class="input-control"
          type="text"
          placeholder="用户名"
          name=""
          id=""
          v-model="username"
        />
      </div>
      <div class="form-group">
        <input
          class="input-control"
          type="password"
          placeholder="密码"
          name=""
          id=""
          v-model="password"
        />
      </div>
      <button
        class="submit login-btn"
        :disabled="!username || !password"
        @click="handleLogin({ username, password })"
      >
        <span>登陆</span>
      </button>
    </div>
  </div>
</template>

<script>
import { mapActions } from "vuex";
export default {
  name: "Login",

  data() {
    return {
      username: "",
      password: ""
    };
  },

  methods: {
    ...mapActions("user", ["handleLogin"])
  }
};
</script>
<style lang="scss">
@import "./index.scss";
</style>
