<script setup>
import { ref } from 'vue';

const text = ref('這是一段文字');
const city = ref('台中市');
const isChecked = ref(true);
const arrayChecked = ref([]);
</script>

<template>
  <div>
    <h1>{{ text }}</h1>
    <input type="text" v-model="text">
  </div>
  <hr>
  {{ city }}
  <select name="" id="" v-model="city">
    <option value="台北市">台北市</option>
    <option value="台中市">台中市</option>
    <option value="台南市">台南市</option>
  </select>
  <hr>
  {{ isChecked }}
  <input type="checkbox" v-model="isChecked">
  <hr>
  {{ arrayChecked }}
  <input type="checkbox" v-model="arrayChecked" value="小夫">
  <input type="checkbox" v-model="arrayChecked" value="小明">
  <input type="checkbox" v-model="arrayChecked" value="胖虎">
</template>
