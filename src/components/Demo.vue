<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <h1>一個人的訊息</h1>
  <h2>姓名: {{ name }}</h2>
  <h2>年紀: {{ age }}</h2>
  <h3>工作種類: {{ job.type }}</h3>
  <h3>薪資: {{ job.salary }}</h3>
  <button @click="sayHello">說話</button>
  <button @click="changeInfo">更改訊息</button>
  <button @click="test">觸發App自定義事件</button>
</template>

<script>
import { ref, reactive } from "vue";
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Demo",
  props: ["msg", "school"],
  emits: ['hello'],
  
  setup(props,context) {
    console.log('props:',props,'context:',context);
    
    // 配置數據
    let name = ref("dennis");
    let age = ref(18);
    let job = reactive({
      type: "前端工程師",
      salary: "30K",
    });

    // 配置方法
    function sayHello() {
      alert(`我叫${name.value},今年${age.value}歲,你好啊!!!`);
    }

    function changeInfo() {
      name.value = "林柏宏";
      age.value = 20;
      job.type = "後端工程師";
      job.salary = "18K";
    }

    function test () {
      context.emit('hello',666)
    }

    return {
      name,
      age,
      sayHello,
      changeInfo,
      job,
      test
    };
  },
};
</script>

<style>
</style>