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
