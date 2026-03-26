<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
    categories: Array
})

const search = ref('')
const category = ref('')
const sort = ref('')

const emit = defineEmits(['update-filters'])

watch([search, category, sort], () => {
    emit('update-filters', {
        search: search.value,
        category: category.value,
        sort: sort.value
    })
})
</script>


<template>
    <div class="filterbar-div">
        <h2>Filters</h2>

        <input v-model="search" placeholder="Search product" />

        <select v-model="category">
            <option value="">All Categories</option>
            <option v-for="cat in props.categories" :key="cat" :value="cat">{{ cat }}</option>
        </select>

        <select v-model="sort">
            <option value="">No Sort</option>
            <option value="price-asc">Price Ascending</option>
            <option value="price-desc">Price Descending</option>
            <option value="rating-desc">Rating Descending</option>
        </select>
    </div>
</template>

<style>
.filterbar-div {
    border: 1px solid gray;
    padding: 10px;
    margin: 10px 0;
}
</style>