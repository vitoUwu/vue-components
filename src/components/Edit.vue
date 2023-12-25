<script setup lang="ts">
defineProps<{ hide: boolean }>();
</script>

<template>
  <span
    :class="{
      'visible opacity-100': !hide,
      'invisible opacity-0': hide,
    }"
    class="text-xs transition-all cursor-pointer"
  >
    ✏️
  </span>
</template>
