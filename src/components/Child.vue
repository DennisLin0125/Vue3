<template>
  <div class="child">
    <h3>我是Child組件</h3>
    <Son/>
  </div>
</template>

<script>
import Son from './Son.vue';
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Child',
    components:{Son}
}
</script>

<style>
.child {
    background-color: skyblue;
    padding: 10px;
}
</style>