<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div>
    <h1>當前的和為 : {{ sum }}</h1>
    <button @click="sum++">點我+1</button>
    <hr />
    <h2>當前鼠標座標為: X : {{ point.x }} Y: {{ point.y }}</h2>
  </div>
</template>

<script>
import { ref } from "vue";
import usePoint from "../hooks/usePoint";
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Demo",
  setup() {
    let sum = ref(0);

    let point = usePoint();

    return {
      sum,
      point
    };
  },
};
</script>
