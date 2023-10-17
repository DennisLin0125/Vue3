<template>
  <div class="child">
    <h3>我是Child組件</h3>
    {{ sum }}
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Child",
  async setup() {
    let sum = ref(0);
    let p = new Promise((resolve) => {
      setTimeout(() => {
        resolve({ sum });
      }, 1000);
    });
    return await p;
  },
};
</script>

<style>
.child {
  background-color: skyblue;
  padding: 10px;
}
</style>