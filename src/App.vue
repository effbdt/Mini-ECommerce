<script setup>
import { products } from './data/products';
</script>

<template>
  <h1>Products</h1>

  <ul>
    <li v-for="p in products" :key="p.id">
      {{ p.name }} - {{ p.price }}
    </li>
  </ul>

</template>

<style>

</style>