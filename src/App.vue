<script setup>
import { computed, ref } from 'vue'
import { products } from './data/products';
import ProductList from './components/ProductList.vue';
import CartSummary from './components/CartSummary.vue';
import FiltersBar from './components/FiltersBar.vue';

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

const filters = ref({
  search: '',
  category: '',
  sort: ''
})

const categories = computed(() => [...new Set(products.map(p => p.category))])

const filteredProducts = computed(() => {
  let result = [...products]

  //search
  if (filters.value.search) {
    result = result.filter(p =>
      p.name.toLowerCase().includes(filters.value.search.toLowerCase())
    )
  }

  //category
  if (filters.value.category) {
    result = result.filter(p => p.category === filters.value.category)
  }

  //sort
  if (filters.value.sort === 'price-asc') {
    result.sort((a, b) => a.price - b.price)
  } else if (filters.value.sort === 'price-desc') {
    result.sort((a, b) => b.price - a.price)
  } else if (filters.value.sort === 'rating-desc') {
    result.sort((a, b) => b.rating - a.rating)
  }

  return result

})

</script>

<template>
  <h1>Mini E-Commerce Shop</h1>

  <FiltersBar @update-filters="filters = $event" :categories="categories" />

  <CartSummary :cart="cart" :products="products" />

  <ProductList 
  :products="filteredProducts"
  @add-to-cart="addToCart"/>
 

</template>

<style>
h1{
  text-align: center;
  padding: 15px 0;
}
</style>