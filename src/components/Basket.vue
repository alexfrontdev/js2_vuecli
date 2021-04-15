<template>
  <div>
    <button class="cart-button" type="button" @click="closeCart">
      Корзина
    </button>
    <div class="cart" v-bind:class="{ 'd-none': isVisibleCart }">
      КОРЗИНА:
      <div v-for="good in accamulateProducts" :key="good.id_product">
        <div class="cart_item">
          {{ good[0].product_name }} {{ good.length }}
        </div>
      </div>
      <button class="closeCart" @click="closeCart">x</button>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    addedProducts: {
      type: Array,
      required: true,
    },
  },
  data: () => ({
    isVisibleCart: true,
  }),
  computed: {
    accamulateProducts() {
      return this.addedProducts.reduce((result, currentProduct) => {
        (result[currentProduct["id_product"]] =
          result[currentProduct["id_product"]] || []).push(currentProduct);
        return result;
      }, {});
    },
  },
  methods: {
    closeCart() {
      console.log(this.isVisibleCart);
      this.isVisibleCart = !this.isVisibleCart;
    },
  },
};
</script>

<style scoped>
.cart {
  padding: 20px;
  position: fixed;
  right: 0;
  top: 50px;
  background: rgb(241, 241, 241);
  width: 500px;
}

.closeCart {
  position: fixed;
  top: 55px;
  right: 5px;
}
.cart-button {
  position: fixed;
  left: 10px;
  top: 10px;
}
.d-none {
  display: none;
}
</style>