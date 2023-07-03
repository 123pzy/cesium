<template>
  <div v-for="(item, index) in list" class="item" :key="index">
    <div>{{ item.name }}</div>
  </div>
  <button @click="add" v-teleport="false">push</button>
</template>

<script setup>
import { ref, nextTick } from "vue";
const list = ref([{ name: 1 }, { name: 2 }]);

function add() {
  list.value.push({ name: 3 });
}
console.log(123);
</script>

<style scoped></style>
