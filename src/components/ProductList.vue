<script setup>
import ProductCard from './ProductCard.vue'

const props = defineProps({
    products: Array
})

const emit = defineEmits(['add-to-cart'])
</script>

<template>
    <div class="productList-div">
        <ProductCard v-for="p in products" :key="p.id" :product="p" @add-to-cart="emit('add-to-cart', $event)" />
    </div>
</template>

<style>
.productList-div{
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
}
</style>
