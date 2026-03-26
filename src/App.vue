<script setup>
import { ref } from 'vue'
import { products } from './data/products';
import ProductCard from './components/ProductCard.vue';
import CartSummary from './components/CartSummary.vue';

const cart = ref([])

function addToCart(productId) {
  const existing = cart.value.find(i => i.id === productId)

  if (existing) {
    existing.quantity++
  } else {
    cart.value.push({ id: productId, quantity: 1 })
  }

  console.log(cart.value)
}

</script>

<template>
  <h1>Products</h1>

  <CartSummary :cart="cart" :products="products"/>


  <ProductCard v-for="p in products" :key="p.id" :product="p"
  @add-to-cart="addToCart" />

</template>

<style></style>