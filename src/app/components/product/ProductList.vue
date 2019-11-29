<template>
  <div id="products" class="box">
    <div class="products--header has-text-centered">
      <i class="fa fa-2x fa-user-circle"></i>
    </div>
    <div class="product-list" v-for="productItem in productItems" :key="productItem.id">
      <ProductListItem :productItem="productItem" />
    </div>
    <div class="product-count has-text-right">
      <span class="has-text-weight-bold"># of products: {{productItemsCount}}</span>
    </div>
  </div>
</template>

<script>
// import { mapGetters } from "vuex";
import ProductListItem from "./ProductListItem";
export default {
  name: "ProductList",
  components: {
    ProductListItem
  },
  computed: {
    productItems() {
      return this.$store.getters.productItems;
    },
    productItemsCount() {
      return this.$store.getters.productItemsCount;
    }
    // ...mapGetters(["productItems", "productItemsCount"])
  },
  created() {
    this.$store.dispatch("getProductItems");
  }
};
</script>

<style>
.box .products--header {
  border-bottom: 1px solid #e8e8e8;
  padding-bottom: 15px;
}

.box .product-list {
  padding-top: 10px;
}
</style>
