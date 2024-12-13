<template>
  <div>
    <h2>Categories</h2>
    <ul>
      <li v-for="category in categories" :key="category">{{ category }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'CateGories',
  props: {
    categories: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
/* Add categories-specific styles here */
</style>
