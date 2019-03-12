<template>
  <div>
    <h1>Product List</h1>
    <img
      v-if="loading"
      src="https://i.imgur.com/JfPpwOA.gif"
    >
    <ul v-else>
      <li v-for="product in products">
        {{product.title}} - {{product.price | currency}} - {{product.inventory}}
        <button
          :disabled="!productIsInStock(product)"
          @click="addProductToCart(product)"
        >Add to cart</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { mapState, mapGetters, mapActions } from 'vuex';

export default {
  computed: {
    ...mapGetters({
      products: 'cartProducts',
      total: 'cartTotal',
    }),
    ...mapState({
      checkoutStatus: state => state.cart.checkoutStatus,
    }),
  },
  methods: {
    ...mapActions(['checkout']),
  },
};
</script>

<style scoped>

</style>
