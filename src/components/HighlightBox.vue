<script setup>
import { computed } from 'vue';
import { products } from '../data/products';

const props = defineProps({
    products: Array
})

const deal = computed(() => {
    if (!props.products.length) return null
    return [...props.products].sort((a, b) => a.price - b.price)[0]
})
</script>


<template>
    <div class="deal-main">
        <h3>Best deal today!</h3>

        <div v-if="deal">
            <img :src="deal.image" width="200px">
            <p><strong>{{ deal.name }}</strong></p>
            <p class="price-p">${{ deal.price }}</p>
            <p>{{ deal.category }}</p>
        </div>

        <div v-else>
            <p>No deals avaliable</p>
        </div>

    </div>
</template>

<style scoped>
.deal-main {
    border: 1px solid #ddd;
    border-radius: 5px;
    background-color: #f9f9f9;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    height: 95%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    width: 80%;
}

.deal-main h3 {
    margin-top: 20px;
    color: #333;
}

.deal-main img {
    border-radius: 5px;
    /* margin: 10px 0; */
}

.price-p {
    color: #e74c3c;
    font-weight: bold;
    font-size: 18px;
}
</style>