# Vue3快速上手

<img src="https://user-images.githubusercontent.com/499550/93624428-53932780-f9ae-11ea-8d16-af949e16a09f.png" style="width:200px" />

## 1.Vue3簡介

- 2020年9月18日，Vue.js發布3.0版本，代號：One Piece（海賊王）
- 耗時2年以上、[2600+次提交](https://github.com/vuejs/vue-next/graphs/commit-activity)、[30+個RFC](<https://github.com/> vuejs/rfcs/tree/master/active-rfcs)、[600+次PR](<https://github.com/vuejs/vue-next/pulls?q=is%3Apr+is%3Amerged+-author%3Aapp%> 2Fdependabot-preview+)、[99位貢獻者](https://github.com/vuejs/vue-next/graphs/contributors)
- github上的tags網址：<https://github.com/vuejs/vue-next/releases/tag/v3.0.0>

## 2.Vue3帶來了什麼

### 1.效能的提升

- 打包大小減少41%

- 初次渲染快55%, 更新渲染快133%

- 記憶體減少54%

   .....

### 2.原始碼的升級

- 使用`Proxy`取代`defineProperty`實作響應式

- 重寫虛擬`DOM`的實作和`Tree-Shaking`

   .....

### 3.擁抱TypeScript

- Vue3可以更好的支援`TypeScript`

### 4.新的特性

1. Composition API（組合API）

    - setup配置
    - ref與reactive
    - watch與watchEffect
    - provide與inject
    - ......
2. 新的內建組件
    - Fragment
    - Teleport
    - Suspense
3. 其他改變

    - 新的生命週期鉤子
    - data 選項應始終被宣告為一個函數
    - 移除keyCode支援作為 v-on 的修飾符
    - ......

# 一、創建Vue3.0工程

## 1.使用 vue-cli 創建

官方文件：<https://cli.vuejs.org/zh/guide/creating-a-project.html#vue-create>

## 查看@vue/cli版本，確保@vue/cli版本在4.5.0以上

```bash
vue --version
```

## 安裝或升級你的@vue/cli

```bash
npm install -g @vue/cli
```

## 創建

```bash
vue create vue_test
```

## 啟動

```bash
cd vue_test
npm run serve
```

## 2.使用 vite 創建

官方文件：<https://v3.cn.vuejs.org/guide/installation.html#vite>

vite官網：<https://vitejs.cn>

- 什麼是vite？ —— 新一代前端建置工具。
- 優點如下：
  - 開發環境中，無需打包操作，可快速的冷啟動。
  - 輕量快速的熱重載（HMR）。
  - 真正的按需編譯，不再等待整個應用程式編譯完成。

## 創建工程

```bash
npm init vite-app <project-name>
```

## 進入工程目錄

```bash
cd <project-name>
```

## 安裝依賴

```bash
npm i
```

## 運行

```bash
npm run dev
```

# 二、常用 Composition API

官方文件: <https://v3.cn.vuejs.org/guide/composition-api-introduction.html>

## 1.拉開序幕的setup

1. 理解：Vue3.0中一個新的配置項，值為一個函數。
2. setup是所有`Composition API（組合API）`「表演的舞台」。
4. 元件中所用到的：資料、方法等等，都要配置在setup中。
5. setup函數的兩種回傳值：
    1. 若傳回一個對象，則該對像中的屬性、方法, 在模板中均可直接使用。 （`重點關注`！）
    2. 若回傳一個渲染函數：則可以自訂渲染內容。
6. 注意點：
    1. 盡量不要與Vue2.x配置混用
       - Vue2.x配置（data、methos、computed...）中`可以存取`setup中的屬性、方法。
       - 但在setup中`不能存取`Vue2.x配置（data、methos、computed...）。
       - 如果有重名, setup優先。
    2. setup不能是一個async函數，因為回傳值不再是return的物件, 而是promise, 模板看不到return物件中的屬性。 （後期也可以傳回一個Promise實例，但需要Suspense和非同步組件的配合）

## 2.ref函數

- 作用: 定義一個響應式的數據
- 語法:

```js
const xxx = ref(initValue)
```

- 建立一個包含響應式資料的`引用對象（reference對象，簡稱ref對象）`。
- JS中操作資料：

```js
xxx.value
```

- 模板中讀取資料: 不需要.value，直接：

```js
<div>{{xxx}}</div>
```

- 備註：
- 接收的資料可以是：基本型別、也可以是物件型別。
- 基本類型的資料：響應式依然是靠`Object.defineProperty()`的`get`與`set`完成的。
- 物件類型的資料：內部 「 `求助` 」 了Vue3.0中的一個新函數— `reactive`函數。

## 3.reactive函數

- 作用: 定義一個物件類型的響應式資料（基本型別不要用它，要用`ref`函數）
- 語法：

```js
const 代理對象= reactive(源對象)
```

接收一個對象（或數組），返回一個代理對象（Proxy的實例對象，簡稱proxy對象 ）

- `reactive`定義的響應式資料是「深層的」。
- 內部基於 ES6 的 Proxy 實現，透過代理物件操作來源物件內部資料進行操作。

## 4.Vue3.0中的響應式原理

### vue2.x的響應式

- 實作原理：
  - 物件類型：透過`Object.defineProperty()`對屬性的讀取、修改進行攔截（資料劫持）。
  
  - 數組類型：透過重寫更新數組的一系列方法來實現攔截。 （對數組的變更方法進行了包裹）。
  
     ```js
     Object.defineProperty(data, 'count', {
         get () {},
         set () {}
     })
     ```

- 存在問題：
  - 新增屬性、刪除屬性, 介面不會更新。
  - 直接透過下標修改陣列, 介面不會自動更新。

### Vue3.0的響應式

- 實現原理:
  - 透過Proxy（代理）: 攔截物件中任意屬性的變化, 包括：屬性值的讀寫、屬性的新增、屬性的刪除等。
  - 透過Reflect（反射）: 對來源物件的屬性進行操作。
  - MDN文檔中所描述的Proxy與Reflect：
    - Proxy：<https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy>

    - Reflect：<https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect>

    ```js
    new Proxy(data, {
    // 攔截讀取屬性值
        get (target, prop) {
        return Reflect.get(target, prop)
        },
        // 攔截設定屬性值或新增屬性
        set (target, prop, value) {
        return Reflect.set(target, prop, value)
        },
        // 攔截刪除屬性
        deleteProperty (target, prop) {
        return Reflect.deleteProperty(target, prop)
        }
    })
    
    proxy.name = 'tom'
    ```

## 5.reactive對比ref

- 從定義資料角度比較：
  - ref用來定義：基本類型資料。
  - reactive用來定義：物件（或陣列）類型資料。
  - 備註：ref也可以用來定義物件（或陣列）類型資料, 它內部會自動透過`reactive`轉為`代理物件`。
- 從原理角度比較：
  - ref透過`Object.defineProperty()`的`get`與`set`來實現響應式（資料劫持）。
  - reactive透過使用來實現響應式（資料劫持）, 並透過`Reflect`操作來源物件內部的資料。
- 從使用角度比較：
  - ref定義的資料：操作資料需要`.value`，並且讀取資料時模板直接讀取不需要`.value`。
  - reactive定義的資料：操作資料與讀取資料：皆不需要`.value`。

## 6.setup的兩個注意點

- setup執行的時機
  - 在beforeCreate之前執行一次，this是undefined。
  
- setup的參數
  - props：值為對象，包含：元件外部傳遞過來，且元件內部聲明接收了的屬性。
  - context：上下文對象
    - attrs: 值為對象，包含：組件外部傳遞過來，但沒有在props配置中聲明的屬性, 相當於

    ```js
    this.$attrs
    ```

    - slots: 收到的插槽內容, 相當於

    ```js
    this.$slots
    ```

    - emit: 分發自訂事件的函數, 相當於

    ```js
    this.$emit
    ```

## 7.計算屬性與監視

### 1.computed函數

- 與Vue2.x中computed配置功能一致

- 寫法

   ```js
   import {computed} from 'vue'
  
   setup(){
       …
   //計算屬性——簡寫
       let fullName = computed(()=>{
           return person.firstName + '-' + person.lastName
       })
       //計算屬性－完整
       let fullName = computed({
           get(){
               return person.firstName + '-' + person.lastName
           },
           set(value){
               const nameArr = value.split('-')
               person.firstName = nameArr[0]
               person.lastName = nameArr[1]
           }
       })
   }
   ```
