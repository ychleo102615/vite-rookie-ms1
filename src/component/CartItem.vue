<template>
  <li class="list-group-item d-flex justify-content-between align-items-center">
    <div>
      <h6 class="my-0">{{ cartItem.name }}</h6>
      <small class="text-muted">數量：{{ cartItem.quantity }}</small>
    </div>
    <div>
      <span class="text-muted">${{ totalPrice }}</span>
      <button @click="onRemoveItem" class="btn btn-sm btn-outline-danger ms-2">移除</button>
    </div>
  </li>
</template>

<script setup>
import { defineProps, defineEmits, computed } from 'vue'

const props = defineProps({
  cartItem: {
    type: Object,
    required: true,
  },
})

const emits = defineEmits(['removeItem'])

const totalPrice = computed(() => {
  return props.cartItem.price * props.cartItem.quantity
})

const onRemoveItem = () => {
  emits('removeItem', props.cartItem.id)
}
</script>

<style scoped></style>
