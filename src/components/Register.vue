<template>
  <div class="register">
    <h2>Регистрация</h2>
    <form @submit.prevent="register">
      <div>
        <label for="fio">ФИО:</label>
        <input type="text" id="fio" v-model="fio" required />
      </div>
      <div>
        <label for="email">Почта:</label>
        <input type="email" id="email" v-model="email" required />
      </div>
      <div>
        <label for="password">Пароль:</label>
        <input type="password" id="password" v-model="password" required />
      </div>
      <hr />
      <button type="submit">Зарегистрироваться</button>
    </form>
    <p v-if="error">{{ error }}</p>
  </div>
</template>

<script>
import axios from 'axios';
const API_HOST = 'http://lifestealer86.ru/api-shop';

export default {
  name: 'Signup',
  data() {
    return {
      fio: '',
      email: '',
      password: '',
      error: null,
    };
  },
  methods: {
    async register() {
      try {
        const response = await axios.post(`${API_HOST}/signup`, {
          fio: this.fio,
          email: this.email,
          password: this.password,
        }, {
          headers: {
            'Content-Type': 'application/json',
          },
        });

        if (response.status === 201) {
          const token = response.data.data.user_token;
          // Сохраните токен в Vuex Store или localStorage
          this.$store.dispatch('AUTH_REQUEST', {token});
          this.$router.push('/login');
        }
      } catch (error) {
        if (error.response && error.response.data) {
          this.error = error.response.data.message || 'Ошибка регистрации';
        } else {
          this.error = 'Произошла ошибка на сервере';
        }
      }
    },
  },
};
</script>

<style scoped>
.register {
  max-width: 400px;
  margin: 0 auto;
}
.register button{
  font-family: Garamond, sans-serif;
}
form div {
  margin-bottom: 10px;
}
label {
  display: block;
  margin-bottom: 5px;
}
input {
  width: 100%;
  padding: 8px;
  border-radius: 5px;
  box-sizing: border-box;
}
button {
  width: 100%;
  padding: 10px;
  background-color: rgba(11, 156, 49, .2);
  border-radius: 5px;
  color: black;
  border: none;
  cursor: pointer;
}
button:hover {
  background-color: pink;
}
</style>