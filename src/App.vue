<script setup>
import { products } from './data/products';
import ProductCard from './components/ProductCard.vue';
</script>

<template>
  <h1>Products</h1>

  <ProductCard v-for="p in products" :key="p.id" :product="p" />

</template>

<style></style>