<script setup lang="ts">
import { PhDotsThree, PhPencil, PhTrash } from "@phosphor-icons/vue";
import { computed, ref } from "vue";
import Edit from "./Edit.vue";

defineProps<{ title: string; category: string; unicode: string }>();

const mode = ref<"none" | "edit" | "delete" | "context">("none");
const contextButtonStyle = computed(() => ({
  "bg-zinc-900/50": mode.value !== "none",
  "opacity-0 invisible": mode.value === "edit",
}));
const buttonsContainer = computed(() => ({
  "translate-y-1/2 bottom-1/2": mode.value !== "edit",
  "right-[52px] opacity-100": mode.value === "context",
  "-right-20 opacity-0": mode.value === "none",
  "bottom-3 right-3": mode.value === "edit",
}));
const deleteButtonStyle = computed(() => ({
  "opacity-0 invisible": mode.value === "edit",
  "opacity-100": mode.value !== "edit",
}));

const titleRef = ref<HTMLParagraphElement | null>(null);
const categoryRef = ref<HTMLParagraphElement | null>(null);
</script>

<template>
  <div
    class="relative w-full p-3 transition-all border rounded-lg border-zinc-900 overflow-clip"
    :class="[mode === 'edit' ? 'pb-11' : 'pb-3']"
  >
    <div class="flex justify-between gap-3 group">
      <div
        class="flex w-full gap-3 overflow-y-visible overflow-x-clip"
        :style="{
          '-webkit-mask':
            'linear-gradient(90deg, white, white 95%, transparent)',
          mask: 'linear-gradient(90deg, white, white 95%, transparent)',
        }"
      >
        <div
          class="flex shrink-0 items-center justify-center border rounded border-orange-600/5 bg-orange-900/[0.1] size-11 select-none"
        >
          <img
            alt="Icon"
            width="25"
            height="25"
            loading="eager"
            :title="title"
            :src="`https://cdn.jsdelivr.net/gh/twitter/twemoji@latest/assets/72x72/${unicode}.png`"
          />
        </div>
        <div class="flex flex-col">
          <div class="flex items-center gap-3">
            <p
              ref="titleRef"
              :contenteditable="mode === 'edit'"
              :tabindex="mode === 'edit' ? 0 : -1"
              class="font-extrabold transition-all group-hover:text-zinc-200 focus:outline-none focus:ring-2 focus:ring-zinc-600 focus:ring-offset-1 focus:ring-offset-zinc-900 focus:rounded-md focus:px-3 line-clamp-1 focus:mb-3 focus:mt-1"
              :class="[
                mode === 'edit' ? 'cursor-pointer focus:cursor-text' : '',
              ]"
            >
              {{ title }}
            </p>
            <Edit @click="titleRef?.focus()" :hide="mode !== 'edit'" />
          </div>
          <div class="flex items-center gap-3">
            <p
              ref="categoryRef"
              :contenteditable="mode === 'edit'"
              :tabindex="mode === 'edit' ? 0 : -1"
              class="text-sm font-medium transition-all text-zinc-600 focus:outline-none focus:ring-2 focus:ring-zinc-600 focus:ring-offset-1 focus:ring-offset-zinc-900 focus:rounded-md focus:px-3 line-clamp-1 focus:mt-3 focus:mb-1"
            >
              {{ category }}
            </p>
            <Edit @click="categoryRef?.focus()" :hide="mode !== 'edit'" />
          </div>
        </div>
      </div>
      <button
        @click="mode = mode === 'context' ? 'none' : 'context'"
        class="flex items-center self-center justify-center transition-all rounded size-8 hover:bg-zinc-900/50 active:bg-zinc-900/70"
        :class="contextButtonStyle"
      >
        <PhDotsThree size="25" class="stroke-current stroke-[15]" />
      </button>
      <div
        :style="{
          '-webkit-mask': 'linear-gradient(90deg, transparent, white 25%)',
          mask: 'linear-gradient(90deg, transparent, white 25%)',
        }"
        class="absolute flex items-center gap-2 pl-6 transition-all bg-zinc-950"
        :class="buttonsContainer"
      >
        <button
          class="flex items-center justify-center transition-all rounded size-8 hover:bg-red-900/10 active:bg-red-900/20"
          :class="deleteButtonStyle"
        >
          <PhTrash size="20" class="text-red-600/50" />
        </button>
        <button
          @click="mode = mode === 'edit' ? 'none' : 'edit'"
          class="flex items-center justify-center transition-all rounded hover:bg-zinc-900/50 active:bg-zinc-900/70"
          :class="[
            mode === 'edit'
              ? 'h-8 w-fit px-3 border border-zinc-900'
              : 'size-8 border-transparent ',
          ]"
        >
          <PhPencil
            size="20"
            class="transition-all"
            :class="[mode === 'edit' ? 'hidden opacity-0' : 'opacity-100']"
          />
          <p
            class="text-sm font-semibold transition-all text-zinc-300"
            :class="[mode === 'edit' ? 'opacity-100' : 'hidden opacity-0']"
          >
            Done
          </p>
        </button>
      </div>
    </div>
  </div>
</template>
