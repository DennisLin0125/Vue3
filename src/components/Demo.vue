<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div>
    <h1>當前的和為 : {{ sum }}</h1>
    <button @click="sum++">點我+1</button>
  </div>
</template>

<script>
import { 
    ref,
    onBeforeMount,
    onMounted,
    onBeforeUpdate,
    onUpdated,
    onBeforeUnmount,
    onUnmounted
 } from "vue";
 
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Demo",
  setup() {
    let sum = ref(0)
    // 通過組合API使用生命鉤子
    onBeforeMount(() => {
         console.log('---onBeforeMount---')   
    })
    onMounted(() => {
        console.log('---onMounted---') 
    })
    onBeforeUpdate(() => {
        console.log('---onBeforeUpdate---') 
    })
    onUpdated(() => {
        console.log('---onUpdated---') 
    })
    onBeforeUnmount(() => {
        console.log('---onBeforeUnmount---') 
    })
    onUnmounted(() => {
        console.log('---onUnmounted---') 
    })

    return {
      sum,
    };
  },
  //   通過配置項使用生命鉤子
//   beforeCreate() {
//     console.log("---beforeCreate---");
//   },
//   created() {
//     console.log("---created---");
//   },
//   beforeMount() {
//     console.log("---beforeMount---");
//   },
//   mounted() {
//     console.log("---mounted---");
//   },
//   beforeUpdate() {
//     console.log("---beforeUnmount---");
//   },
//   updated() {
//     console.log("---updated---");
//   },
//   beforeUnmount() {
//     console.log("---beforeUnmount---");
//   },
//   unmounted() {
//     console.log("---unmounted---");
//   },
};
</script>
