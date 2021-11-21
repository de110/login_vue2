<template>
  <div>
    <h1>Login</h1>
    <div>
      <label for="username">사용자 이름: </label>
      <input type="text" id="username" v-model="credentials.username" />
    </div>
    <div>
      <label for="password">비밀번호: </label>
      <input type="password" id="password" v-model="credentials.password" />
    </div>

    <button @click="login">login</button>
  </div>
</template>

<script>
import axios from "axios";

// const SERVER_URL = process.env.VUE_APP_SERVER_URL

export default {
  name: "Login",
  data: function() {
    return {
      credentials: {
        username: null,
        password: null
      }
    };
  },
  methods: {
    login: function() {
      axios({
        method: "post",
        url: "http://localhost:8080/authenticate",
        data: this.credentials
      })
        .then(res => {
          // 로컬스토리지에 토큰 저장
          localStorage.setItem("jwt", res.data.token);
          // TodoList로 이동
          this.$router.push({ name: "Home" });
        })
        .catch(err => {
          console.log(err);
        });
    }
  }
};
</script>
