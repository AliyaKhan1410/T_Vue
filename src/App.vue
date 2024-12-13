<template>
  <div>
    <Navbar />
    <main>
      <p v-if="loading">Loading...</p>
      <p v-else-if="error">{{ error }}</p>
      <template v-else>
        <Categories :categories="categories" />
        <ImageGrid :products="products" />
      </template>
    </main>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import Navbar from './components/Navbar.vue';
import Categories from './components/Categories.vue';
import ImageGrid from './components/ImageGrid.vue';

export default {
  components: {
    Navbar,
    Categories,
    ImageGrid,
  },
  setup() {
    const products = ref([]);
    const categories = ref([]);
    const loading = ref(true);
    const error = ref(null);

    onMounted(async () => {
      try {
        const productResponse = await fetch('https://fakestoreapi.com/products');
        const categoryResponse = await fetch('https://fakestoreapi.com/products/categories');

        if (!productResponse.ok || !categoryResponse.ok) {
          throw new Error('Failed to fetch data');
        }

        products.value = await productResponse.json();
        categories.value = await categoryResponse.json();
        loading.value = false;
      } catch (err) {
        console.error(err);
        error.value = 'Failed to load data. Please try again later.';
        loading.value = false;
      }
    });

    return { products, categories, loading, error };
  },
};
</script>

<style scoped>
/* Add your app-specific styles here */
</style>
