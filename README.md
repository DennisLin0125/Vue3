# 其它 Composition API

## 1.shallowReactive 與 shallowRef

- shallowReactive：只處理物件最外層屬性的響應式（淺響應式）。
- shallowRef：只處理基本資料類型的響應式, 不進行物件的響應式處理。

- 什麼時候使用?
  - 如果有一個物件數據，結構比較深, 但變化時只是外層屬性變化 ===> shallowReactive。
  - 如果有一個物件數據，後續功能不會修改該物件中的屬性，而是生新的物件來替換 ===> shallowRef。

## 2.readonly 與 shallowReadonly

- readonly: 讓一個響應式資料變成唯讀的（深只讀）。
- shallowReadonly：讓一個響應式資料變成唯讀的（淺只讀）。
- 應用場景: 不希望資料被修改時。

## 3.toRaw 與 markRaw

- toRaw：
  - 作用：將一個由`reactive`生成的`反應式物件`轉為`普通物件` 。
  - 使用場景：用於讀取響應式物件對應的普通對象，對這個普通物件的所有操作，不會造成頁面更新。
- markRaw：
  - 作用：標記一個對象，使其永遠不會再成為響應式對象。
  - 應用場景:
     1. 有些值不應被設定為響應式的，例如複雜的第三方類別庫等。
     2. 當渲染具有不可變資料來源的大列表時，跳過響應式轉換可以提高效能。

## 4.customRef

- 作用：建立一個自訂的 ref，並對其依賴項追蹤和更新觸發進行明確控制。

- 實現防手震效果：

```vue
<template>
    <input type="text" v-model="keyword">
    <h3>{{keyword}}</h3>
</template>

<script>
import {ref,customRef} 從 'vue'
export default {
    name:'Demo',
    setup(){
        // let keyword = ref('hello') //使用Vue準備好的內建ref
        //自訂一個myRef
        function myRef(value,delay){
            let timer;
            //透過customRef去實現自訂
            return customRef((track,trigger)=>{
                return{
                    get(){
                        track(); //告訴Vue這個value值是需要被「追蹤」的
                        return value;
                    },
                    set(newValue){
                        clearTimeout(timer);
                        timer = setTimeout(()=>{
                            value = newValue;
                            trigger() //告訴Vue去更新介面
                        },delay);
                    }
                }
            })
        }

        let keyword = myRef('hello',500) //使用程式設計師自訂的ref
        return {
            keyword
        }
    }
}
</script>
```
