<script setup>
import MerchCard from './component/MerchCard.vue'
import Cart from './component/Cart.vue'
import Notification from './component/Notification.vue'

import { ref } from 'vue'

const merchs = ref([
  {
    id: 1,
    name: '耳罩式藍牙耳機',
    description: '舒適配戴，支援降噪技術',
    price: 2490,
    image:
      'https://images.unsplash.com/photo-1546435770-a3e426bf472b?q=80&w=2065&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA==',
  },
])

const onMerchAdded = (merch) => {
  // 在這裡處理加入購物車的邏輯
  console.log('加入購物車:', merch)
}
</script>

<template>
  <div id="app" class="container py-4">
    <div class="row">
      <!-- 商品列表區 -->
      <div class="col-md-8">
        <h2 class="mb-3">商品列表</h2>
        <div class="row">
          <MerchCard
            @addMerch="onMerchAdded"
            v-for="merch in merchs"
            :key="merch.id"
            :merch="merch"
          />
        </div>
      </div>
      <Cart />
    </div>
    <Notification />
  </div>
</template>

<style scoped>
.card-img-top {
  height: 150px;
  object-fit: cover;
}
</style>
