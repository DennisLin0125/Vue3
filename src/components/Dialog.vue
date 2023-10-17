<template>
  <div>
    <button @click="isShow = true">點我彈窗</button>
    <Teleport to="body">
      <div v-if="isShow" class="mask">
        <div class="dialog">
          <h3>我是一個彈窗</h3>
          <h4>一些內容</h4>
          <h4>一些內容</h4>
          <h4>一些內容</h4>
          <h4>一些內容</h4>
          <button @click="isShow = false">關閉彈窗</button>
        </div>
      </div>
    </Teleport>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Dialog",
  setup() {
    let isShow = ref(false);

    return { isShow };
  },
};
</script>

<style>
.mask {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.5);
}
.dialog {
  position: absolute;
  text-align: center;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  height: 300px;
  width: 300px;
  background-color: green;
}
</style>