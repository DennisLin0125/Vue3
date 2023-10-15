<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <h1>當前求和為: {{ sum }}</h1>
  <button @click="sum++">點我加1</button>
  <hr />
  <h2>當前的信息為: {{ msg }}</h2>
  <button @click="msg += '!'">修改訊息</button>
</template>

<script>
import { ref, watch } from "vue";
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Demo",
  // watch: {
  //   // sum(newValue,oldValue) {
  //   //   console.log('sum的值變了',newValue,oldValue)
  //   // }
  //   sum: {
  //     immediate:true,
  //     deep:true,
  //     handler(newValue,oldValue){
  //       console.log('sum的值變了',newValue,oldValue)
  //     }
  //   }
  // },

  setup() {
    // 配置數據
    let sum = ref(0);
    let msg = ref("你好");

    // 情況1 監視ref所定義的1個響應式數據
    // watch([msg], (newValue, oldValue) => {
    //   console.log("sum的值變了", newValue, oldValue);
    // });

    // 情況2 監視ref所定義的多個響應式數據
    watch([msg,sum], (newValue, oldValue) => {
      console.log("msg的值變了", newValue, oldValue);
    },{immediate:true,});

    return {
      sum,
      msg,
    };
  },
};
</script>

<style>
</style>