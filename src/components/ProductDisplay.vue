<template>
  <div v-if="isLoading" class="container">
    {{ console.log(isLoading) }}
    <div class="product__container">
      <div class="product__image skeleton">image</div>
      <div class="product__content">
        <div>
          <h3 class="product__title skeleton">title</h3>
          <div class="product__rating skeleton">rating</div>
          <hr>
          <p class="product__description skeleton">description</p>
        </div>
        <div>
          <hr>
          <p class="product__price skeleton">price</p>
          <div class="product__action">
            <button class="primary-button skeleton">Buy Now</button>
            <button class="secondary-button skeleton">Next Product</button>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div v-else class="container">
    {{ console.log(data.product) }}
    <div class="product__container">
      <img :src="data.product.image" class="product__image" alt="product-image" />
      <div class="product__content">
        <div>
          <h3 class="product__title">{{ data.product.title }}</h3>
          <div style="display: flex; justify-content: space-between; align-items: center; font-size: 18px;">
            <p class="product__category">{{ data.product.category }}</p>
            <div class="product__rating">
              <span>{{ data.product.rating.rate }}</span>
              <div>
                <span class="dot"></span>
                <span class="dot"></span>
                <span class="dot"></span>
                <span class="dot"></span>
                <span class="dot"></span>
              </div>
            </div>
          </div>
          <hr>
          <p class="product__description">{{ data.product.description }}</p>
        </div>
        <div>
          <hr>
          <p class="product__price">${{ data.product.price }}</p>
          <div class="product__action">
            <button class="primary-button">Buy Now</button>
            <button class="secondary-button" @click="getProductById()">Next Product</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductDisplay',
  data () {
    return {
      isLoading: false,
      index: 0,
      data: {}
    }
  },
  methods: {
    async callAPI() {
      const response = await fetch(`https://fakestoreapi.com/products/${this.index}`);
      const result = await response.json();

      return result;
    },
    async getProductById() {
      this.isLoading = true;
      this.index == 20 ? (this.index = 1) : this.index++;

      let product = await this.callAPI();

      this.data = { product }

      this.isLoading = false;
    },
  },
  created() {
    this.getProductById();
  }
}
</script>
<style>
@import '../assets/style/page.css';
</style>