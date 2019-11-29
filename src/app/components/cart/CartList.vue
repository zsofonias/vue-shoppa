<template>
  <div id="cart" class="cart">
    <div class="cart--header has-text-centered">
      <i class="fa fa-2x fa-shopping-cart"></i>
    </div>
    <ul>
      <li v-for="cartItem in cartItems" :key="cartItem.id" class="cart-item">
        <CartListItem :cartItem="cartItem" />
      </li>
      <div class="cart-details" v-if="cartItemsCount > 0">
        <p>
          Total Quantity:
          <span class="has-text-weight-bold">{{cartItemsCount}}</span>
        </p>
        <p class="cart-remove-all--text" @click="removeAllCartItems">
          <i class="fa fa-trash"></i>Remove all
        </p>
      </div>
      <div class="cart-details" v-else>
        <p>Cart Empty!, Add Items To Cart</p>
      </div>
    </ul>
    <button class="button is-primary" :disabled="!cartItemsCount">
      Checkout (
      <span class="has-text-weight-bold">${{cartTotalPrice}}</span>)
    </button>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";
import CartListItem from "./CartListItem";
export default {
  name: "CartList",
  components: {
    CartListItem
  },
  methods: {
    // removeCartItems() {
    //   this.$store.dispatch("removeAllCartItems");
    // }
    ...mapActions(["removeAllCartItems"])
  },
  computed: {
    // cartItems() {
    //   return this.$store.getters.cartItems;
    // },
    // cartItemsCount() {
    //   return this.$store.getters.cartItemsCount;
    // },
    // cartTotalPrice() {
    //   return this.$store.getters.cartTotalPrice;
    // },
    ...mapGetters(["cartItems", "cartItemsCount", "cartTotalPrice"])
  },
  created() {
    this.$store.dispatch("getCartItems");
  }
};
</script>

<style>
#cart {
  height: 100%;
  padding: 30px 10px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.cart .cart-item {
  padding: 10px 0;
}

.cart .cart-empty-text {
  padding: 10px 0;
}

.cart .cart--header {
  border-bottom: 1px solid #e8e8e8;
  padding-bottom: 15px;
}

.cart .cart-details {
  font-size: 12px;
  display: flex;
  justify-content: space-between;
  padding: 15px;
}

.cart .cart-remove-all--text {
  cursor: pointer;
}

.cart .cart-remove-all--text .fa {
  padding-right: 5px;
}
</style>
