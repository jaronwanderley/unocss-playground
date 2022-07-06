<script setup lang="ts"></script>

<template>
  <nav
    class="
      p-2
      mx-4
      transition-all
      duration-250
      ease-soft-in
      rounded-2xl
      lg:flex-nowrap lg:justify-start
      sticky
      top-0
      bg-white
      shadow-blur
      z-110
    "
  >
    <slot />
  </nav>
</template>
