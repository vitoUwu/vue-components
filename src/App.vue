<script setup lang="ts">
import Item from "./components/Item.vue";
</script>

<template>
  <!-- Give someone a program; you frustrate them for a day; teach them how to program, and you frustrate them for a lifetime -->
  <div class="flex items-center justify-center h-dvh bg-zinc-950 text-zinc-300">
    <div
      class="flex flex-col items-stretch justify-center w-full h-full gap-3 px-6 max-w-96"
    >
      <Item category="Food" title="Hamburguer" unicode="1f354" />
      <Item category="Food" title="Pizza" unicode="1f355" />
      <Item category="Food" title="Cookies" unicode="1f36a" />
      <Item category="Food" title="Ice Cream" unicode="1f368" />
    </div>
  </div>
</template>
