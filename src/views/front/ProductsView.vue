<template>
    <div class="my-5">
        <div class="row row-cols-1 row-cols-md-3 g-4">
          <div class="col" v-for="productItem in products" :key="productItem.id">
            <div class="card h-100">
              <img :src="productItem.imageUrl"
              class="img-fluid card-img-top2" :alt="productItem.title" />
              <div class="card-body">
                <h5 class="card-title">{{productItem.title}}</h5>
                <p class="card-text">
                 {{ productItem.description }}
                </p>
              </div>
              <div class="card-footer bg-transparent">
                <RouterLink :to="`/products/${productItem.id}`">查看更多</RouterLink>
              </div>
            </div>
          </div>
        </div>
    </div>
</template>
<style>
        .table-transparent{
            background-color: transparent !important;
        }
        .table-image{
            height: 100px;
            width: 100px;
            object-fit: cover;
        }
        .card-img-top2{
            height: 200px;
            object-fit: cover;
        }
</style>
<script>
import axios from 'axios';

const { VITE_APP_API_URL, VITE_APP_API_NAME } = import.meta.env;

export default {
  data() {
    return {
      products: [],
      pages: {},
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
          this.pages = res.data.pagination;
        })
        .catch((err) => {
          alert(`${err.data.message}`);
        });
    },
  },
  mounted() {
    this.getProducts();
  },
};
</script>
