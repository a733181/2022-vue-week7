<template>
  <div class="mb-10 hero">
    <div class="flex flex-col items-center justify-center h-full text-white">
      <h1 class="mb-2 text-5xl font-bold">小農種植</h1>
      <h2 class="mb-6 text-3xl font-bold">產地直送，安心食用</h2>
      <router-link to="/products">
        <base-btn class="w-[300px]">前往購買</base-btn>
      </router-link>
    </div>
  </div>
  <div class="container px-4 mx-auto mb-12">
    <ul class="flex flex-col items-center justify-center gap-9 lg:flex-row lg:items-start">
      <li class="w-[400px]">
        <img
          src="https://cdn.pixabay.com/photo/2015/09/20/07/21/dirt-947985_960_720.jpg"
          alt="土地"
          class="w-full mb-3 rounded-lg"
        />

        <h3 class="mb-2 text-3xl">有機農業</h3>
        <p>
          有機農業是一種能維護土壤、生態系統和人類健康的生產體系，遵從當地的生態節律、生物多樣性和自然循環，而不依賴會帶來不利影響的投入物質。
        </p>
      </li>
      <li class="w-[400px]">
        <img
          src="https://cdn.pixabay.com/photo/2020/03/05/09/20/gunny-sack-4903874_960_720.jpg"
          alt="麻袋"
          class="w-full mb-3 rounded-lg"
        />

        <h3 class="mb-2 text-3xl">環保包裝</h3>
        <p>包裝產品採用可回收材質，降低包材對環境的負擔。</p>
      </li>
      <li class="w-[400px]">
        <img
          src="https://cdn.pixabay.com/photo/2020/03/15/12/50/truck-4933514_960_720.jpg"
          alt="貨車"
          class="w-full mb-3 rounded-lg"
        />
        <h3 class="mb-2 text-3xl">產地直送</h3>
        <p>與貨運公司合作，專車配送，送貨到府</p>
      </li>
    </ul>
  </div>
  <div class="mb-12 bg-gray-100">
    <div class="container flex flex-col items-center justify-center p-4 px-6 mx-auto lg:flex-row">
      <h3 class="mb-2 lg:mr-6 lg:mb-0">
        限時限量優惠代碼，數量有限送完為止，結帳時請自行輸入折扣碼：
        <span class="font-bold">leafGo</span>
      </h3>
      <router-link to="/products">
        <base-btn class="w-[300px]">前往購買</base-btn>
      </router-link>
    </div>
  </div>
  <div class="container px-4 mx-auto">
    <product-more title="熱銷商品" :product-data="productsData"></product-more>
  </div>
</template>

<script>
import ProductMore from '../../components/forestage/product/ProductMore.vue';

export default {
  components: { ProductMore },
  computed: {
    productsData() {
      return this.$store.getters['forestageProducts/productsData'];
    },
  },
  methods: {
    async getProducts() {
      try {
        this.isLoading = true;
        await this.$store.dispatch('forestageProducts/getProducts');
      } catch (err) {
        this.error = err;
      } finally {
        this.isLoading = false;
      }
    },
  },
  mounted() {
    this.getProducts();
  },
};
</script>

<style scoped>
.hero {
  background-image: linear-gradient(rgba(0, 0, 0, 0.3), rgba(0, 0, 0, 0.3)),
    url('https://cdn.pixabay.com/photo/2014/02/12/18/11/lettuce-264826_960_720.jpg');
  width: 100%;
  height: 600px;
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;
}
</style>
