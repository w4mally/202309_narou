<script setup lang="ts">
import { ref } from 'vue'

/* 型の定義 */
interface Item {
    name: string
    price: number
}

const items = ref<Item[]>([
    { name: 'egg', price: 100 },
    { name: 'apple', price: 100}
])

const newItemName = ref('')
const newItemPrice = ref('')

const addItem = () => {
    if( newItemName.value === '' || newItemPrice.value === 0) return
    items.value.push({ name: newItemName.value, price: newItemPrice.value })
    newItemName.value = ''
    newItemPrice.value = 0
}
</script>

<template>
    <div>
        <div>ItemList</div>
        <ul>
         <li v-for="item in items" :key="item.name" :class="{ over500: item.price >= 500}">
            <div>name: {{ item.name }}</div>
            <div>{{ item.price }} yen</div>
            <div v-if="item.price >= 10000">expensive!!</div>
         </li>
        </ul>
        <div>
            <label>
                name
                <input v-model="newItemName" type="text" />
            </label>
            <label>
                price
                <input v-model="newItemPrice" type="number" />
            </label>
            <button @click="addItem">add</button>
        </div>
    </div>
</template>

<style>
.over500 {
    color: red;
}
</style>