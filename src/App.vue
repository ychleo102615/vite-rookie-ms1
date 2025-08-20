<script setup>
import MerchLineUp from './component/MerchLineUp.vue'
import Cart from './component/Cart.vue'
import Notification from './component/Notification.vue'
</script>

<template>
  <div id="app" class="container py-4">
    <div class="row">
      <MerchLineUp />
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
