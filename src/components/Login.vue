<template>
  <form class="login" @submit.prevent="login">
    <h1>Авторизация</h1>
    <label for="email">Почта:</label>
    <input type="email" id="email" v-model="email" required />
    <label>Пароль:</label>
    <input type="password" required v-model="password" />
    <hr />
    <button type="submit">Войти</button>
  </form>
</template>

<script>
import axios from 'axios';
const API_HOST = 'http://lifestealer86.ru/api-shop';

export default {
  data() {
    return {
      email: "",
      password: "",
      error: null,
    };
  },
  methods: {
    async login() {
      try {
        const response = await axios.post(`${API_HOST}/login`, {
          email: this.email,
          password: this.password,
        }, {
          headers: {
            'Content-Type': 'application/json',
          },
        });

        if (response.status === 200) {
          const token = response.data.data.user_token;
          // Сохраните токен в Vuex Store или localStorage
          this.$store.dispatch('AUTH_REQUEST', {token});
          this.$router.push('/');
        } else {
          this.error = 'Неверный email или пароль';
        }
      } catch (error) {
        if (error.response && error.response.data) {
          this.error = error.response.data.message || 'Ошибка авторизации';
        } else {
          this.error = 'Произошла ошибка на сервере';
        }
      }
    },
  },
};
</script>

<style scoped>
.login {
  display: flex;
  flex-direction: column;
  max-width: 400px;
  margin: 0 auto;
}
.login input, button {
  width: 100%;
  padding: 8px;
  border-radius: 5px;
  box-sizing: border-box;
  font-family: Garamond, sans-serif;
}
button {
  width: 100%;
  padding: 10px;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
}
button:hover {
  background-color: #0056b3;
}
hr {
  margin: 10px 0;
}
</style>