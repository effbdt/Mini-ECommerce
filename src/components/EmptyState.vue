<script setup>
const props = defineProps({
    message: {
        type: String,
        default: "No products found"
    }
})
</script>

<template>
    <div>
        <h2>{{ message }}</h2>
        <p>Filters returned nothing</p>
    </div>
</template>

<style scoped>
div {
    padding: 40px 20px;
    text-align: center;
    color: #666;
    background-color: #f9f9f9;
    border-radius: 5px;
    border: 1px solid #ddd;
    margin: 20px 0;
}

h2 {
    margin: 0 0 10px 0;
    color: #333;
}

p {
    margin: 0;
    font-size: 14px;
}
</style>