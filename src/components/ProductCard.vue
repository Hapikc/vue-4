<template>
  <div class="product-card">
    <img
        :src="getFullImageUrl(product.image)"
        alt="Product Image"
        class="product-image"
        @error="handleImageError"
    />
    <h3>{{ product.name || 'No Title' }}</h3>
    <p>{{ product.description || 'No Description' }}</p>
    <p><strong>Цена: {{ product.price }} Руб</strong></p>
    <button @click="addToCart">Добавить в корзину</button>
  </div>
</template>

<script>
import Header from "@/components/Header.vue";

export default {
  components: {Header},
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
  methods: {
    addToCart() {
      this.$store.dispatch('addToCart', this.product);
    },

    getFullImageUrl(imagePath) {
      const baseUrl = 'http://lifestealer86.ru/';
      return `${baseUrl}${imagePath}`;
    },
  },
};
</script>

<style scoped>
.product-card {
  padding: 16px;
  margin: 8px;
  width: 300px;
  text-align: center;
  flex-direction: column;
  border: 1px solid #ccc;
  border-radius: 8px;
  background-color: #f9f9f9;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.product-card button:hover{
  background: pink;
  border: 2px solid gray;
}
.product-image {
  max-width: 100%;
  height: auto;
  margin-bottom: 8px;
  border-radius: 10px;
}
.product-card button{
  padding: 10px;
  border-radius: 5px;
  font-family: Garamond, sans-serif;
  background-color: rgba(11, 156, 49, .2);
  border: 2px solid black;
}
</style>