<template>
  <nav aria-label="Page navigation example">
    <ul class="pagination justify-content-center">
      <li class="page-item" :class="{ disabled: !pages.has_pre }">
        <a class="page-link" aria-label="Previous">
          <span aria-hidden="true" @click="getProducts(pages.current_page - 1)"
            >&laquo;</span
          >
        </a>
      </li>
      <!-- 為何key要加123?
      因page為索引數值，vue官方說不建議用索引直接當值，所以加上其他數值，避免問題 -->
      <li
        class="page-item"
        v-for="page in pages.total_pages"
        :key="page + 123"
        :class="{ active: page === pages.current_page }"
      >
        <a class="page-link" @click="getProducts(page)">{{ page }}</a>
      </li>
      <!-- 動態屬性
      要加入目前所在頁面按鈕有active樣式，需綁定樣式
    v-blind:class插入物件 { 套用Class名稱 : 判斷式 } -->
      <li class="page-item" :class="{ disabled: !pages.has_next }">
        <a class="page-link" aria-label="Next">
          <span aria-hidden="true" @click="getProducts(pages.current_page + 1)"
            >&raquo;</span
          >
        </a>
      </li>
    </ul>
  </nav>
</template>
<script>
export default {
  props: ['pages', 'getProducts'],
};
</script>
