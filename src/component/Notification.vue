<template>
  <!-- 通知元件 -->
  <transition-group
    tag="div"
    name="fade"
    class="position-fixed bottom-0 end-0 p-3"
    style="z-index: 1050"
  >
    <div
      v-for="context in notifications"
      :key="context.id"
      class="toast show align-items-center text-white border-0 mb-2"
      :class="{
        'bg-success': context.type === 'add',
        'bg-secondary': context.type === 'delete',
        'bg-primary': context.type === 'update',
      }"
    >
      <div class="d-flex">
        <div class="toast-body">{{ context.message }}</div>
        <button
          type="button"
          class="btn-close btn-close-white me-2 m-auto"
          @click="emits('closeNotification', context.id)"
        ></button>
      </div>
    </div>
  </transition-group>
</template>

<script setup>
import { inject, defineEmits } from 'vue'

const notifications = inject('notifications')
const emits = defineEmits(['closeNotification'])
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-leave-active {
  pointer-events: none;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
