<script setup>
const props = defineProps({
    product: Object
})

const emit = defineEmits(['add-to-cart'])

function handleClick() {
    emit('add-to-cart', props.product.id)
}
</script>

<template>
    <div class="product-card">
        <img :src="product.image" width="120" />

        <h3>{{ product.name }}</h3>
        <p>Price: ${{ product.price }}</p>
        <p>Category: {{ product.category }}</p>
        <p>Rating: {{ product.rating }}⭐</p>

        <button :disabled="!product.inStock" @click="handleClick" class="cart-button">
            {{ product.inStock ? "Add to Cart" : "Out of stock" }}
        </button>
    </div>

</template>

<style>
.product-card {
    width: 200px;
    min-height: 250px;
    border: 1px solid #ccc;
    padding: 6px;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    background-color: #e6f7ff;
    border-radius: 5px;
}
.product-card img {
    align-self: center;
    border-radius: 5px;
}

.cart-button{
    background-color: rgb(85, 240, 85);
    padding: 8px;
    border: rgb(162, 255, 162) 5px;
    border-radius: 5px;
    font-weight: bold;
}

.cart-button:hover{
    background-color: rgb(0, 200, 0);
}

.cart-button:active {
    transform: translateY(1.5px);
}


</style>