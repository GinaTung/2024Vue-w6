<template>
  <div
    id="productModal"
    ref="productModal"
    class="modal fade"
    tabindex="-1"
    aria-labelledby="productModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog modal-xl">
      <div class="modal-content border-0">
        <div class="modal-header bg-dark text-white">
          <h5 id="productModalLabel" class="modal-title">
            <span>{{ isNew ? "新增產品" : "編輯產品" }}</span>
          </h5>
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body">
          <div class="row">
            <div class="col-sm-4">
              <div class="mb-2">
                <div class="mb-3">
                  <label for="imageUrl" class="form-label">輸入圖片網址</label>
                  <input
                    type="text"
                    v-model="editProduct.imageUrl"
                    class="form-control"
                    placeholder="請輸入圖片連結"
                  />
                </div>
                <img class="img-fluid" :src="editProduct.imageUrl" alt="" />
              </div>
              <!-- 多圖設置 -->
              <!-- 判斷 editProduct.imagesUrl"是一個陣列-->
              <div v-if="Array.isArray(editProduct.imagesUrl)">
                <div
                  v-for="(item, key) in editProduct.imagesUrl"
                  :key="key + 123"
                >
                  <img :src="item" alt="" class="img-fluid my-2" />
                  <input
                    type="text"
                    class="form-control"
                    v-model="editProduct.imagesUrl[key]"
                  />
                </div>
                <!-- v-if 判斷沒有圖片時顯示或有點選新增圖片未填寫完成網址時 -->
                <button
                  class="btn btn-outline-primary btn-sm d-block w-100"
                  v-if="
                    editProduct.imagesUrl.length === 0 ||
                    editProduct.imagesUrl[editProduct.imagesUrl.length - 1]
                  "
                  @click="editProduct.imagesUrl.push('')"
                >
                  新增圖片
                </button>
                <button
                  v-else
                  class="btn btn-outline-danger btn-sm d-block w-100"
                  @click="editProduct.imagesUrl.pop()"
                >
                  刪除圖片
                </button>
              </div>
              <div class="pt-3">
                <input
                  type="file"
                  class="form-control"
                  id="file"
                  ref="fileInput"
                  placeholder="請輸入圖片連結"
                  @change="upload"
                />
              </div>
              <div></div>
            </div>
            <div class="col-sm-8">
              <!-- <pre>
                {{editProduct}}
              </pre> -->
              <div class="mb-3">
                <label for="title" class="form-label">標題</label>
                <input
                  id="title"
                  type="text"
                  v-model="editProduct.title"
                  class="form-control"
                  placeholder="請輸入標題"
                />
              </div>

              <div class="row">
                <div class="mb-3 col-md-6">
                  <label for="category" class="form-label">分類</label>
                  <input
                    id="category"
                    type="text"
                    v-model="editProduct.category"
                    class="form-control"
                    placeholder="請輸入分類"
                  />
                </div>
                <div class="mb-3 col-md-6">
                  <label for="price" class="form-label">單位</label>
                  <input
                    id="unit"
                    type="text"
                    v-model="editProduct.unit"
                    class="form-control"
                    placeholder="請輸入單位"
                  />
                </div>
              </div>

              <div class="row">
                <div class="mb-3 col-md-6">
                  <label for="origin_price" class="form-label">原價</label>
                  <input
                    id="origin_price"
                    type="number"
                    v-model="editProduct.origin_price"
                    min="0"
                    class="form-control"
                    placeholder="請輸入原價"
                  />
                </div>
                <div class="mb-3 col-md-6">
                  <label for="price" class="form-label">售價</label>
                  <input
                    id="price"
                    type="number"
                    v-model="editProduct.price"
                    min="0"
                    class="form-control"
                    placeholder="請輸入售價"
                  />
                </div>
              </div>
              <hr />

              <div class="mb-3">
                <label for="description" class="form-label">產品描述</label>
                <textarea
                  id="description"
                  type="text"
                  v-model="editProduct.description"
                  class="form-control"
                  placeholder="請輸入產品描述"
                >
                </textarea>
              </div>
              <div class="mb-3">
                <label for="content" class="form-label">說明內容</label>
                <textarea
                  id="description"
                  type="text"
                  v-model="editProduct.content"
                  class="form-control"
                  placeholder="請輸入說明內容"
                >
                </textarea>
              </div>
              <div class="mb-3">
                <div class="form-check">
                  <input
                    id="is_enabled"
                    class="form-check-input"
                    type="checkbox"
                    v-model="editProduct.is_enabled"
                    :true-value="1"
                    :false-value="0"
                  />
                  <label class="form-check-label" for="is_enabled"
                    >是否啟用</label
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="modal-footer">
          <button
            type="button"
            class="btn btn-outline-secondary"
            data-bs-dismiss="modal"
          >
            取消
          </button>
          <button type="button" class="btn btn-primary" @click="updateProduct">
            確認
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { Modal } from 'bootstrap';

export default {
  props: ['tempProduct', 'updateProduct', 'isNew', 'upload', 'score', 'tempRating'],
  data() {
    return {
      modalProduct: null,
      editProduct: {},
      tempRatingStar: {},
    };
  },
  watch: {
    tempProduct() {
      this.editProduct = this.tempProduct;
    },

  },
  methods: {
    openModal() {
      this.modalProduct.show();
    },
    closeModal() {
      this.modalProduct.hide();
    },

  },
  mounted() {
    this.modalProduct = new Modal(this.$refs.productModal);
    this.editProduct = this.tempProduct;
  },
};
</script>
