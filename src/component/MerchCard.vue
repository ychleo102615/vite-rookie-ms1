<template>
  <div class="col-md-4 mb-4">
    <div class="card h-100">
      <img :src="merch.image" class="card-img-top" />
      <div class="card-body">
        <h5 class="card-title">{{ merch.name }}</h5>
        <p class="card-text">{{ merch.description }}</p>
        <p class="fw-bold text-primary">$ {{ merch.price }}</p>
        <button class="btn btn-success w-100" @click="onClickCartBtn">加入購物車</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

const emits = defineEmits(['addMerch'])

const props = defineProps({
  merch: {
    type: Object,
    required: true,
  },
})

const onClickCartBtn = () => {
  emits('addMerch', props.merch)
}
</script>

<style scoped></style>
