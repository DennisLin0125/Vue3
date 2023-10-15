<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <h1>一個人的訊息</h1>
  姓:<input type="text" v-model="person.firstName" />
  <br />
  名:<input type="text" v-model="person.lastName" />
  <br />
  <br />
  <span>全名:{{ person.fullName }}</span>
  <br />
  全名: <input type="text" v-model="person.fullName" />
</template>

<script>
import { reactive, computed } from "vue";
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Demo",

  setup() {
    // 配置數據
    let person = reactive({
      firstName: "張",
      lastName: "三",
    });

    // 計算屬性
    person.fullName = computed({
      get() {
        return person.firstName + "-" + person.lastName;
      },
      set(value) {
        const arr = value.split("-");
        person.firstName = arr[0];
        person.lastName = arr[1];
      },
    });

    return {
      person,
    };
  },
};
</script>

<style>
</style>