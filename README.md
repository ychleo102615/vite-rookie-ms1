[原作業連結](https://rpg.hexschool.com/#/tasks/12062817613343793189)

# 作業內容

任務描述
完成以下畫面中，將商品加入購物車的功能（[版型可參考模板](https://codepen.io/hexschool/pen/EaVwgmK)）

![](https://images.hexschool.com/common/MTc1Mzc2NDQzNDQ4MzQ1Mjg0NDc=_2025-07-12T15:33:31Z.jpeg)

需求功能描述

- 請嘗試將「商品列表」、「購物車」、「通知」拆分成 3 個元件
- 請使用 props 將商品資料傳遞至「商品列表」元件
- 「購物車」元件的刪除功能，請使用 emit 傳遞事件
- 使用 provide, inject 完成通知功能

<br>

# 作業回饋

- 同學少了總金額的金額的計算可以使用，提醒同學可以使用 computd 搭配 reduce() 進行累加。
- MerchCard 中商品的圖片建議加上 alt 敘述，記得使用 v-bind:alt 做綁定
- MerchCard 建議可以改命名為 ProductCard，較符合網頁中代表商品區域的意思
- 可以將新增通知的邏輯獨立成一個方法，讓結構更清楚一點，如:

```js
const pushNotification = (message, type) => {
  notifyCount++
  const context = {
    removed: false,
    id: notifyCount,
    message: message,
    type: type,
  }
  notifications.value.push(context)
  setTimeout(() => {
    removeNotification(context.id)
  }, waitDur)
}
```
