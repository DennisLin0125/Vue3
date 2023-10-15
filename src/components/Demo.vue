<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <h1>當前求和為: {{ sum }}</h1>
  <button @click="sum++">點我加1</button>
  <hr />
  <h2>當前的信息為: {{ msg }}</h2>
  <button @click="msg += '!'">修改訊息</button>
  <h2>名字: {{ person.name }}</h2>
  <h2>年齡: {{ person.age }}</h2>
  <button @click="person.name += '~'">修改名字</button>
  <button @click="person.age++">修改年齡</button>
</template>

<script>
import { reactive, watch, ref, watchEffect } from "vue";
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
    let person = reactive({
      name: "張三",
      age: 18,
    });

    watchEffect(() => {
      const x1 = sum.value
      const x2 = person.name
      console.log('watchEffect所指定的回調執行了')
    })

    return {
      sum,
      msg,
      person,
    };
  },
};
</script>

<style>
</style>