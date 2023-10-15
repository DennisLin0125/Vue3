<template>
  <Demo @hello="showHello" msg="hello" school="MIT"/>
</template>

<script>
import Demo from './components/Demo'
export default {
  name: "App",
  components: {Demo},
  setup(){
    function showHello(value){
      return alert(`你觸發了hello事件,收到的參數是${value}`)
    }

    return {
      showHello
    }
  }
};
</script>

