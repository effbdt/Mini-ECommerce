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
    <div>
        <img :src="product.image" width="120" />

        <h3>{{ product.name }}</h3>
        <p>Price: ${{ product.price }}</p>
        <p>Category: {{ product.category }}</p>
        <p>Rating: {{ product.rating }}⭐</p>

        <button :disabled="!product.inStock" @click="handleClick">
            {{ product.inStock ? "Add to Cart" : "Out of stock" }}
        </button>
    </div>

</template>