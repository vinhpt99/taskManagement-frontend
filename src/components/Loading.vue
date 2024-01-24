<template>
  <div v-if="isLoading" class="loading">
    <div
      class="inline-block h-14 w-14 animate-spin rounded-full border-4 border-solid border-current border-r-transparent align-[-0.125em] motion-reduce:animate-[spin_1.5s_linear_infinite]"
      role="status">
      <span
        class="!absolute !-m-px !h-px !w-px !overflow-hidden !whitespace-nowrap !border-0 !p-0 ![clip:rect(0,0,0,0)]">Loading...</span>
    </div>
  </div>
</template>
<script setup>
defineProps({
  isLoading: {
    type: Boolean,
    default: false
  }
})
</script>
<style>
.loading {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  /* Màu nền có độ mờ */
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 9999;
}
</style>