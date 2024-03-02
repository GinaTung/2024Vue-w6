<template>
  <div v-for="productItem in products" :key="productItem.id">
    <div v-if="id === productItem.id">
      <h1 class="my-3">{{ productItem.title }}</h1>
      <div class="row">
        <div class="col-12 col-md-6">
          {{ productItem.description }}
          {{ productItem.content }}
        </div>
        <div class="col-12 col-md-6">
          <img :src="productItem.imageUrl" :alt="productItem.title" class="img-fluid">
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios';

const { VITE_APP_API_URL, VITE_APP_API_NAME } = import.meta.env;
export default {
  data() {
    return {
      id: '',
      products: [],
      productData: [],
    };
  },
  methods: {
    getProducts(page = 1) { // 參數預設值
      // 有分頁
      axios
        .get(`${VITE_APP_API_URL}/api/${VITE_APP_API_NAME}/products/all?page=${page}`)
        .then((res) => {
          console.log(res);
          this.products = res.data.products;
          this.products.forEach((item) => {
            if (this.id === item.id) this.productData.push(item);
          });
        })
        .catch((err) => {
          alert(`${err.data.message}`);
        });
    },
  },
  mounted() {
    // console.log(this.$route.params.id);
    this.id = this.$route.params.id;
    this.getProducts();
  },
};
</script>
