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

        <div class="filter_title">
            <img src="https://images.emojiterra.com/twitter/v14.0/512px/1f50e.png" alt="mglass" width="20px">
            <h2>Filters</h2>
        </div>



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
    border: 1px solid #ddd;
    padding: 15px;
    margin: 10px 0;
    border-radius: 5px;
    background-color: #f9f9f9;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.filter_title{
    display: flex;
    align-items: center;
    margin-bottom: 12px;
}

.filter_title h2 {
    margin: 0;
    margin-left: 8px;
}

input{
    margin-right: 10px;
    padding: 8px 12px;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-size: 14px;
}

input:focus {
    outline: none;
    border-color: #007bff;
    box-shadow: 0 0 3px rgba(0, 123, 255, 0.3);
}

select{
    margin-right: 10px;
    padding: 8px 12px;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-size: 14px;
    background-color: white;
}

select:focus {
    outline: none;
    border-color: #007bff;
    box-shadow: 0 0 3px rgba(0, 123, 255, 0.3);
}
</style>