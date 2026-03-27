<script setup>
import { computed, ref } from 'vue'
import { products } from './data/products';
import ProductList from './components/ProductList.vue';
import CartSummary from './components/CartSummary.vue';
import FiltersBar from './components/FiltersBar.vue';
import HighlightBox from './components/HighlightBox.vue';

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
  <div class="parent">
    <div class="div1">
      <h1>Mini E-Commerce Shop</h1>
    </div>
    <div class="div2">
      <FiltersBar @update-filters="filters = $event" :categories="categories" />
    </div>
    <div class="div3">
      <CartSummary :cart="cart" :products="products" />
    </div>
    <div class="div4">
      <HighlightBox :products="products" />
    </div>
    <div class="div5">
      <ProductList :products="filteredProducts" @add-to-cart="addToCart" />
    </div>
  </div>
</template>

<style>
h1 {
  text-align: center;
  padding: 15px 0;
}

.parent {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: auto auto auto auto;
  gap: 10px;
  margin: 20px;
}

.div1 {
  grid-area: 1 / 1 / 2 / 3;
}

.div2 {
  grid-area: 2 / 1 / 3 / 2;
}

.div3 {
  grid-area: 3 / 1 / 4 / 2;
}

.div4 {
  grid-area: 2 / 2 / 4 / 3;
}

.div5 {
  grid-area: 4 / 1 / 5 / 3;
}

body {
  font-family: 'Roboto', sans-serif;
}
</style>