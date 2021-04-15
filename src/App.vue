<template>
  <div id="app">
    <main>
      <search @searched-text="searchText = $event"></search>
      <div class="catalog">
        <div
          v-for="product in filteredProducts"
          :key="product.id_product"
          class="card"
        >
          <p>{{ product.product_name }}</p>
          <p>{{ product.price }}</p>

          <button @click="addToCart(product)">добавить в корзину</button>
        </div>
      </div>

      <basket :added-products="basketProducts"></basket>
    </main>
  </div>
</template>

<script>
import Basket from "./components/Basket.vue";
import Search from "./components/Search.vue";

export default {
  API_URL:
    "https://raw.githubusercontent.com/GeekBrainsTutorial/online-store-api/master/responses/",
  components: {
    Basket,
    Search,
  },
  data() {
    return {
      allProducts: [],
      basketProducts: [],
      searchText: "",
    };
  },
  methods: {
    addToCart(product) {
      this.basketProducts.push({ ...product });
    },
  },
  computed: {
    filteredProducts() {
      return this.allProducts.filter((product) =>
        product.product_name
          .toLowerCase()
          .includes(this.searchText.toLowerCase())
      );
    },
  },
  created() {
    fetch(`${this.$options.API_URL}/catalogData.json`)
      .then((response) => {
        return response.json();
      })
      .then((data) => {
        this.allProducts = data;
      });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
