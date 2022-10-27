<template>
  <div class="product">
    <div class="product-image">
      <img :src="image" />
    </div>

    <div class="product-info">
      <h1>{{ product }}</h1>
      <p v-if="inStock">In Stock</p>
      <p v-else>Out of Stock</p>

      <shipping-tab :shipping="shipping" :details="details"></shipping-tab>

      <ul>
        <li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
      </ul>

      <div
        class="color-box"
        v-for="(variant, index) in variants"
        :key="variant.variantId"
        :style="{ backgroundColor: variant.variantColor }"
        @mouseover="updateProduct(index)"
      ></div>

      <button
        @click="addToCart"
        :disabled="!inStock"
        :class="{ disabledButton: !inStock }"
      >
        Add to Cart
      </button>

      <product-tabs :reviews="reviews"></product-tabs>
    </div>
  </div>
</template>
<script>
import ShippingTab from "./shippingTab.vue";
import ProductTabs from "./tabs.vue";

export default {
  props: {
    premium: {
      type: Boolean,
      required: true,
    },
  },
  components: {
    ShippingTab,
    ProductTabs
  },
  data() {
    return {
      product: "Socks",
      brand: "Vue Mastery",
      selectedVariant: 0,
      details: ["80% cotton", "20% polyester", "Gender-neutral"],
      variants: [
        {
          variantId: 2234,
          variantColor: "green",
          variantImage: "/img/greensock.jpg",
          variantQuantity: 10,
        },
        {
          variantId: 2235,
          variantColor: "Blue",
          variantImage: "/img/bluesock.jpg",
          variantQuantity: 0,
        },
      ],
      reviews: [],
      errors: []
    };
  },
  methods: {
    addToCart() {
      this.$emit("add-to-cart", this.variants[this.selectedVariant].variantId);
    },
    updateProduct(index) {
      this.selectedVariant = index;
    },
  },
  computed: {
    title() {
      return this.brand + " " + this.product;
    },
    image() {
      return this.variants[this.selectedVariant].variantImage;
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity;
    },
    shipping() {
      if (this.premium) {
        return "Free";
      }
      return 2.99;
    },
  },
  mounted() {
    this.$root.$on("review-submitted", (productReview) => {
      this.reviews.push(productReview);
    });
  },
};
</script>

<style>
.product .product-image img {
  max-width: 200px;
}
</style>