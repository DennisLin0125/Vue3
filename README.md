# toRef

- 作用：建立一個 ref 對象，其value值指向另一個對像中的某個屬性。
- 語法：

```js
const name = toRef(person,'name')
```

- 應用: 要將響應式物件中的某個屬性單獨提供給外部使用時。

- 擴充：`toRefs` 與`toRef`功能一致，但可以批次建立多個 ref 對象，語法：

```js
toRefs(person)
```
