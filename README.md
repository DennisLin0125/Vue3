# Vue3.0中可以繼續使用Vue2.x中的生命週期鉤子，但有兩個被更名

- `beforeDestroy`改名為 `beforeUnmount`
- `destroyed`改名為 `unmounted`
- Vue3.0也提供了 Composition API 形式的生命週期鉤子，與Vue2.x中鉤子對應關係如下：
  - `beforeCreate`  ===> `setup()`
  - `created`   =======> `setup()`
  - `beforeMount`   ===> `onBeforeMount`
  - `mounted`   =======> `onMounted`
  - `beforeUpdate`  ===> `onBeforeUpdate`
  - `updated`   =======> `onUpdated`
  - `beforeUnmount`  ==> `onBeforeUnmount`
  - `unmounted`   =====> `onUnmounted`
