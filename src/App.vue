<template>
  <div id="app" class="container mt-5">
    <h1 class="text-info text-uppercase">Shopping cart App</h1>
    <price value="4.000" />
    <price-slider :sliderStatus="sliderStatus" :maximum.sync="maximum" />
    <product-list :maximum="maximum" :products="products" />
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
// import Price from "./components/Price.vue";
import ProductList from "./components/ProductList.vue";
import PriceSlider from "./components/PriceSlider.vue";

export default {
  name: "app",
  data: function () {
    return {
      maximum: 99,
      products: null, // from the api
      sliderStatus: true,
      cart: [],
    };
  },
  components: {
    FontAwesomeIcon,
    // Price, // price < productList
    ProductList,
    PriceSlider,
  },
  methods: {
    addItem: function (product) {
      var whichProduct;
      var existing = this.cart.filter(function (item, index) {
        if (item.product.id == Number(product.id)) {
          whichProduct = index;
          return true;
        } else {
          return false;
        }
      });

      if (existing.length) {
        this.cart[whichProduct].qty++;
      } else {
        this.cart.push({ product: product, qty: 1 });
      }
    },
  },
  mounted: function () {
    fetch("https://hplussport.com/api/products/order/price")
      .then((response) => response.json())
      .then((data) => {
        this.products = data;
      });
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
