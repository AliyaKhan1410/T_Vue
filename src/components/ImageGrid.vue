<template>
  <div class="image-grid">
    <div v-for="product in products" :key="product.id" class="product">
      <img v-if="product.image" :src="product.image" :alt="product.title" class="product-image" />
      <h3>{{ product.title }}</h3>
      <p>${{ product.price }}</p>
      <p>
        {{ product.description.length > 100 ? product.description.slice(0, 100) + '...' : product.description }}
      </p>
      <button v-if="product.description.length > 100" class="see-more">See More</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ImageGrid',
  props: {
    products: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
/* Add image grid-specific styles here */
.image-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
}

.product {
  border: 1px solid #ddd;
  padding: 16px;
  width: 300px;
}

.product-image {
  width: 100%;
  height: auto;
}

.see-more {
  margin-top: 8px;
  background: #007bff;
  color: white;
  border: none;
  padding: 8px 16px;
  cursor: pointer;
}
</style>
