<template>
  <div :style="fontstyle">{{ rate }}</div>
</template>

<script setup>
import { defineProps, computed } from 'vue';
/**
 * 描述：defineProps 来规范传递数据的格式，这里规定了组件会接收外部传来的 value 属性和theme属性
 * 分别用来修改评分星星数和星星主题颜色
 */
let props = defineProps({
  value: Number,
  theme: {
    type: String,
    default: 'orange'
  }
});
let rate = computed(() =>
  '★★★★★☆☆☆☆☆'.slice(5 - props.value, 10 - props.value)
);
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
