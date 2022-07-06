<script setup lang="ts">
defineProps({
  
})
const showDrawer = $ref(false)
</script>

<template>
  <aside
    class="
      w-full
      max-w-80
      z-990
      fixed
      inset-y-0
      py-4
      pl-4
      transition-transform
      duration-200
      lg:left-0
    "
    :class="{
      'translate-0': showDrawer,
      '-translate-x-full lg:translate-x-0': !showDrawer
    }"
  >
    <slot />
  </aside>
</template>
