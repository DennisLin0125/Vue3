<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div>
    <h2>姓名: {{ name }}</h2>
    <h2>年紀: {{ age }}</h2>
    <h3>薪資: {{ job.j1.salary }}K</h3>
    <button @click="name += '~'">修改姓名</button>
    <button @click="age++">增加年齡</button>
    <button @click="job.j1.salary++">調薪</button>
  </div>
</template>

<script>
import { reactive, toRef, toRefs } from "vue";
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Demo",
  setup() {
    let person = reactive({
      name: "dennis",
      age: 18,
      job: {
        j1: {
          salary: 20,
        },
      },
    });

    return {
      // toRef 方式
      // name: toRef(person, "name"),
      // age: toRef(person, "age"),
      // salary: toRef(person.job.j1, "salary"),

      // toRefs方式
      ...toRefs(person),
    };
  },
};
</script>
