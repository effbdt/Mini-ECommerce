<script setup>
import { computed } from 'vue'

const props = defineProps({
    cart: Array,
    products: Array
})

const totalItems = computed(() =>
    props.cart.reduce((sum, item) => sum + item.quantity, 0)
)

const totalPrice = computed(() => 
    props.cart.reduce((sum, item) => {
        const product = props.products.find(p=> p.id === item.id)
        return sum + (product.price * item.quantity)
    }, 0)
)
</script>


<template>
    <div class="cart-div">
        <h2>Cart Summary</h2>
        <p>Total Items: {{ totalItems }}</p>
        <p>Total Price: {{ totalPrice.toFixed(2) }}</p>
    </div>
</template>

<style>

.cart-div{
    border: 1px solid gray;
    padding: 10px;
    margin: 10px 0;
}
</style>