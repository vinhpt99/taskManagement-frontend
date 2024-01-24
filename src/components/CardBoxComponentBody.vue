<script setup>
defineProps({
  noPadding: Boolean
})
</script>

<template>
  <div style="overflow-y: scroll;" class="flex-1" :class="{ 'p-6': !noPadding } ">
    <slot />
  </div>
</template>
