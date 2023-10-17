<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="son">
    <h3>我是Son組件</h3>
    <Dialog/>
  </div>
</template>

<script>
import Dialog from './Dialog.vue';
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Son",
  components: {Dialog}
};
</script>

<style>
.son {
  background-color: orange;
  padding: 10px;
}
</style>