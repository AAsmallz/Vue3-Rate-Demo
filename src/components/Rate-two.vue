<template>
  <slot></slot>
  <div class="rate" :style="fontstyle">
    <span @mouseover="mouseOver(num)" v-for="num in 5" :key="num">☆</span>
    <span class="hellow" :style="fontWidth">
      <span
        @click="onRate(num)"
        @mouseover="mouseOver(num)"
        v-for="num in 5"
        :key="num"
        >★</span
      >
    </span>
  </div>
</template>
<script setup>
import { ref, defineProps, defineEmits, computed } from 'vue';
let props = defineProps({
  value: Number,
  theme: {
    type: String,
    default: 'orange'
  }
});
console.log(props.theme);
let width = ref(props.value);
// 定义emits
let emits = defineEmits('update-rate');
function mouseOver(i) {
  width.value = i;
}
function mouseOut() {
  width.value = props.value;
}
function onRate(num) {
  // 发射emits时间，在父组件中通过@引用
  emits('update-rate', num);
}
// “em”是一个相对的大小，相对所指的是相对于元素父元素的font-size
const fontWidth = computed(() => `width:${width.value}em`);
const themeObj = {
  black: '#00',
  white: '#fff',
  red: '#f5222d',
  orange: '#fa541c',
  yellow: '#fadb14',
  green: '#73d13d',
  blue: '#40a9ff'
};
const fontstyle = computed(() => {
  return `color:${themeObj[props.theme]};`;
});
</script>

<style scoped>
.rate {
  position: relative;
  display: inline-block;
}
.hellow {
  position: absolute;
  /* 设置才能改变行内元素span宽高 */
  display: inline-block;
  top: 0;
  left: 0;
  /* 设置宽度为0，且超出宽度部分的★不显示 */
  width: 0;
  overflow: hidden;
}
</style>
