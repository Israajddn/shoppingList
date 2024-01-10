<script setup>
import { ref, computed } from 'vue'

let id = 0

const newShoppingItem = ref('')
const hidePurchased = ref(false)
const shoppingItems = ref([
  { id: id++, text: 'Apples', purchased: true },
  { id: id++, text: 'Oranges', purchased: true },
  { id: id++, text: 'Onions', purchased: false },
  { id: id++, text: 'Milk', purchased: false },
  { id: id++, text: 'Lemons', purchased: false }
])

const filteredShoppingItems = computed(() => {
  return hidePurchased.value
    ? shoppingItems.value.filter((t) => !t.purchased)
    : shoppingItems.value
})

function addShoppingItem() {
  shoppingItems.value.push({ id: id++, text: newShoppingItem.value, purchased: false })
  newShoppingItem.value = ''
}

function removeShoppingItem(item) {
  shoppingItems.value = shoppingItems.value.filter((t) => t !== item)
}
</script>

<template>

  <div>
    <h1>My Shopping List:</h1>
  </div>

  <div>
    <form @submit.prevent="addShoppingItem">
      <input v-model="newShoppingItem">
      <button>Add to the Shopping List</button>
    </form>
  </div>

  <div>
    <ul>
      <li v-for="item in filteredShoppingItems" :key="item.id">
        <input type="checkbox" v-model="item.purchased">
        <span :class="{ purchased: item.purchased }">{{ item.text }}</span>
        <button @click="removeShoppingItem(item)">remove</button>
      </li>
    </ul>
  </div>

  <div>
    <button @click="hidePurchased = !hidePurchased">
    {{ hidePurchased ? 'Show all' : 'Hide completed' }}
  </button>
  </div>
 
</template>

<style>
.purchased {
  /* text-decoration: line-through; */
  color: #f6bd60;
}

body {
  background-color: #f7ede2;
  color: #000814;
}

h1 {
  color: #84a59d;
}

button {
  background-color: #f5cac3;
}

ul {
  list-style: none;
}</style>