<template>
    這是後台
    <nav>
        <RouterLink to="/admin/products">產品列表</RouterLink> |
        <RouterLink to="/admin/orders">訂單列表</RouterLink> |
        <RouterLink to="/">回前台</RouterLink> |
    </nav>
    <RouterView></RouterView>
</template>
<script>
import axios from 'axios';

const { VITE_APP_API_URL } = import.meta.env;

export default {
  data() {
    return {
      text: '123',
    };
  },
  methods: {
    checkAdmin() {
      axios
        .post(`${VITE_APP_API_URL}/api/user/check`)
        .then((res) => {
          console.log(res);
        })
        .catch((err) => {
          console.log(err);
          this.$router.push('/login');
        });
    },
  },
  mounted() {
    // 取得cookie資料
    const token = document.cookie.replace(
      /(?:(?:^|.*;\s*)hexToken\s*=\s*([^;]*).*$)|^.*$/,
      '$1',
    );
    axios.defaults.headers.common.Authorization = token;
    // console.log(token);
    this.checkAdmin();
  },
};
</script>
