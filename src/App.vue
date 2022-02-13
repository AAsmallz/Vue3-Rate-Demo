<template>
  <div id="app">
    <h4>评分Demo</h4>
    <!-- <rate-one :value="score" theme="red"></rate-one> -->
    <rate-two :value="score" theme="green" @update-rate="update">
      <p>评分数: {{ score }}</p>
    </rate-two>
  </div>
</template>
<script setup>
import { ref } from 'vue';
import rateOne from './components/Rate-one.vue';
import rateTwo from './components/Rate-two.vue';
let score = ref(4);
function update(num) {
  score.value = num;
}
</script>

<style>
#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 50px;
}
</style>
