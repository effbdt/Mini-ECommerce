<script setup>
import { computed } from 'vue'

const props = defineProps({
    cart: Array,
    products: Array
})

const totalItems = computed(() =>
    props.cart.reduce((sum, item) => sum + item.quantity, 0)
)

const cartItems = computed(() =>
  props.cart
    .map(item => {
      const product = props.products.find(p => p.id === item.id)
      if (!product) return null
      return {
        ...item,
        product,
        lineTotal: product.price * item.quantity
      }
    })
    .filter(Boolean)
)

const totalPrice = computed(() => 
    cartItems.value.reduce((sum, item) => sum + item.lineTotal, 0)
)
</script>


<template>
    <div class="cart-div">
        <h2>Cart Summary</h2>

        <ul>
            <li v-for="item in cartItems" :key="item.id">
                {{ item.product.name }} x {{ item.quantity }} - ${{ item.lineTotal.toFixed(2) }}
            </li>
        </ul>

        <p>Total Items: {{ totalItems }}</p>
        <p>Total Price: ${{ totalPrice.toFixed(2) }}</p>
    </div>
</template>

<style>

.cart-div{
    border: 1px solid gray;
    padding: 10px;
    margin: 10px 0;
}
</style>