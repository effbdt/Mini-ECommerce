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
        <div class="title-div">
            <img src="https://media.istockphoto.com/id/918978530/vector/eco-shopping.jpg?s=612x612&w=0&k=20&c=LPEhpoHnSq46HJ9HkTwpsALSZn4l21gy74aHkwZXMuM="
                alt="shopping_cart" width="40px">
            <h2>Shopping Cart</h2>
        </div>

        <ul>
            <li v-for="item in cartItems" :key="item.id">
                {{ item.product.name }} x {{ item.quantity }} - ${{ item.lineTotal.toFixed(2) }}
            </li>
        </ul>

        <p>Total Items: {{ totalItems }}</p>
        <p>Total Price: ${{ totalPrice.toFixed(2) }}</p>
    </div>
</template>

<style scoped>
.cart-div {
    border: 1px solid #ddd;
    padding: 15px;
    margin: 10px 0;
    border-radius: 5px;
    background-color: #f9f9f9;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.title-div {
    display: flex;
    align-items: center;
    margin-bottom: 12px;
}

.title-div h2 {
    margin: 0;
    margin-left: 8px;
}

ul {
    list-style: none;
    padding: 0;
    margin: 10px 0;
}

li {
    padding: 8px;
    margin: 4px 0;
    background-color: white;
    border-left: 3px solid green;
    border-radius: 3px;
    font-size: 14px;
}

p {
    font-weight: bold;
    margin: 8px 0;
    padding: 8px;
    background-color: white;
    border-radius: 3px;
}
</style>