<script setup>
import MerchCard from './component/MerchCard.vue'
import CartItem from './component/CartItem.vue'
import Notification from './component/Notification.vue'

import { ref, provide } from 'vue'

const waitDur = 2000
const merchs = ref([
  {
    id: 1,
    name: '耳罩式藍牙耳機',
    description: '舒適配戴，支援降噪技術',
    price: 2490,
    image:
      'https://images.unsplash.com/photo-1546435770-a3e426bf472b?q=80&w=2065&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA==',
  },
  {
    id: 2,
    name: '無線藍牙鍵盤',
    description: '輕薄設計，支援多裝置快速切換',
    price: 1290,
    image:
      'https://images.unsplash.com/photo-1587829741301-dc798b83add3?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.1.0',
  },
  {
    id: 3,
    name: '4K 曲面螢幕',
    description: '沉浸式體驗，護眼模式與高刷新率',
    price: 8990,
    image: 'https://img.4gamers.com.tw/news-image/c1bb4832-71fb-42e7-89c1-5f9df66bf1b4.jpg',
  },
  {
    id: 4,
    name: '智慧手錶',
    description: '全天候心率監測，支援GPS與防水設計',
    price: 4990,
    image: 'https://mbzhu.com/wp-content/uploads/2023/10/61OEuoqFqYL-1024x1024.jpg',
  },
  {
    id: 5,
    name: '遊戲滑鼠',
    description: '高精度感應器，RGB 燈效與可編程按鍵',
    price: 1890,
    image: 'https://image.benq.com/is/image/benqco/01-S2C-top-1?$ResponsivePreset$&fmt=png-alpha',
  },
])

const cartItems = ref([])
const notifications = ref([])
/*
context: {
  removed: boolean
  id: number
  message: string
  type: add or delete
}
 */
provide('notifications', notifications)
let notifyCount = 0

const addMerch = (merch) => {
  // 在這裡處理加入購物車的邏輯
  notifyCount++
  let message = ''
  let type = ''
  const cartItem = cartItems.value.find((item) => item.id === merch.id)
  if (cartItem) {
    cartItem.quantity++
    message = '已增加商品數量'
    type = 'update'
  } else {
    cartItems.value.push({
      id: merch.id,
      name: merch.name,
      price: merch.price,
      quantity: 1,
    })
    message = '已加入購物車'
    type = 'add'
  }
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

const removeNotification = (id) => {
  const index = notifications.value.findIndex((x) => x.id == id)
  if (index >= 0) {
    notifications.value.splice(index, 1) // 只移除該索引的單一項目
  }
}

const removeCartItem = (itemId) => {
  const index = cartItems.value.findIndex((item) => item.id === itemId)
  if (index !== -1) {
    cartItems.value.splice(index, 1)
  }
  notifyCount++
  const id = notifyCount
  notifications.value.push({
    removed: false,
    id: id,
    message: '已從購物車移除商品',
    type: 'delete',
  })
  setTimeout(() => {
    removeNotification(id)
  }, waitDur)
}
</script>

<template>
  <div id="app" class="container py-4">
    <div class="row">
      <!-- 商品列表區 -->
      <div class="col-md-8">
        <h2 class="mb-3">商品列表</h2>
        <div class="row">
          <MerchCard @addMerch="addMerch" v-for="merch in merchs" :key="merch.id" :merch="merch" />
        </div>
      </div>

      <!-- 購物車區 -->
      <div class="col-md-4">
        <h2 class="mb-3">購物車</h2>
        <ul class="list-group mb-3">
          <CartItem
            @removeItem="removeCartItem"
            v-for="item in cartItems"
            :key="`cart${item.id}`"
            :cartItem="item"
          />
        </ul>
      </div>
    </div>
    <Notification @closeNotification="removeNotification" />
  </div>
</template>

<style scoped>
.card-img-top {
  height: 150px;
  object-fit: cover;
}
</style>
