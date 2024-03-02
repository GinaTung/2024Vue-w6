<template>
  <div class="container my-5">
    <div class="row justify-content-center">
      <h1 class="h3 mb-3 font-weight-normal text-center">請先登入</h1>
      <div class="col-8">
        <form id="form" class="form-signin" @submit.prevent="login">
          <div class="form-floating mb-3">
            <input
              type="email"
              class="form-control"
              v-model="user.username"
              id="username"
              placeholder="name@example.com"
              required
              autocomplete="username"
            />
            <label for="username">Email address</label>
          </div>
          <div class="form-floating">
            <input
              type="password"
              class="form-control"
              v-model="user.password"
              id="password"
              placeholder="Password"
              required
              autocomplete="current-password"
            />
            <label for="password">Password</label>
          </div>
          <button
            class="btn btn-lg btn-primary w-100 mt-3"
            type="submit"
            id="login"
          >
            登入
          </button>
          <RouterLink class="btn btn-lg btn-dark w-100 mt-3" to="/">回前台</RouterLink>
        </form>
      </div>
    </div>
    <p class="mt-5 mb-3 text-muted text-center">&copy; 2024~∞ - 六角學院</p>
  </div>
</template>

<script>
import axios from 'axios';

const { VITE_APP_API_URL } = import.meta.env;

export default {
  data() {
    return {
      user: {
        email: '',
        password: '',
      },
    };
  },
  methods: {
    login() {
      // const api = import.meta.env.VITE_APP_API_URL;
      axios.post(`${VITE_APP_API_URL}/admin/signin`, this.user)
        .then((res) => {
          // console.log(res);
          const { expired, token } = res.data;
          document.cookie = `hexToken=${token}; expires=${new Date(expired)}`;
          this.$router.push('/admin');
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>
