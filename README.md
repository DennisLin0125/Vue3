# 新的組件

## 1.Fragment

- 在Vue2中: 元件必須有一個根標籤
- 在Vue3中: 元件可以沒有根標籤, 內部會將多個標籤包含在一個Fragment虛擬元素中
- 好處: 減少標籤層級, 減少記憶體佔用

## 2.Teleport

- 什麼是Teleport？ —— `Teleport` 是一種能夠將我們的`元件html結構移到指定位置`的技術。

```vue
<teleport to="移動位置">
    <div v-if="isShow" class="mask">
        <div class="dialog">
            <h3>我是一個彈跳窗</h3>
            <button @click="isShow = false">關閉彈跳窗</button>
        </div>
    </div>
</teleport>
```

## 3.Suspense

- 等待非同步元件時渲染一些額外內容，讓應用程式有更好的使用者體驗

- 使用步驟：

- 非同步引入組件

```js
import {defineAsyncComponent} from 'vue'
const Child = defineAsyncComponent(()=>import('./components/Child.vue'))
```

- 使用`Suspense`包裹組件，並配置好`default` 與 `fallback`

```vue
<template>
    <div class="app">
        <h3>我是App元件</h3>
        <Suspense>

            <template v-slot:default>
                <Child/>
            </template>

            <template v-slot:fallback>
                <h3>載入中.....</h3>
            </template>

        </Suspense>
    </div>
</template>
```

# 其他

## 1.全域API的轉移

- Vue 2.x 有許多全域 API 和設定。
  - 例如：註冊全域元件、註冊全域指令等。

     ```js
     //註冊全域元件
     Vue.component('MyButton', {
       data: () => ({
         count: 0
       }),
       template: '<button @click="count++">Clicked {{ count }} times.</button>'
     })
    
     //註冊全域指令
     Vue.directive('focus', {
       inserted: el => el.focus()
     }
     ```
## 2.其他改變

- data選項應始終被宣告為一個函數。

- 過度類別名稱的更改：

  - Vue2.x寫法

     ```css
     .v-enter,
     .v-leave-to {
       opacity: 0;
     }
     .v-leave,
     .v-enter-to {
       opacity: 1;
     }
     ```

  - Vue3.x寫法

     ```css
     .v-enter-from,
     .v-leave-to {
       opacity: 0;
     }
    
     .v-leave-from,
     .v-enter-to {
       opacity: 1;
     }
     ```

- 移除keyCode作為 v-on 的修飾符，同時也不再支援`config.keyCodes`

- 移除`v-on.nativ`修飾符

  - 父元件中綁定事件

     ```vue
     <my-component
       v-on:close="handleComponentEvent"
       v-on:click="handleNativeClickEvent"
     />
     ```

  - 子元件中聲明自訂事件

     ```vue
     <script>
       export default {
         emits: ['close']
       }
     </script>
     ```

- 移除濾鏡（filter）

   > 過濾器雖然這看起來很方便，但它需要一個自訂語法，打破大括號內表達式是 “只是 JavaScript” 的假設，這不僅有學習成本，而且有實現成本！ 建議用方法呼叫或計算屬性去替換過濾器。
