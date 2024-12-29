<script setup lang="ts">
const slots = useSlots();

const hasSticky = !!slots['sticky'];
</script>

<template>
  <div class="h-screen">
    <div class="flex p-2 h-full">
      <SideBar />
      <div
        class="flex-grow bg-white shadow-lg dark:bg-white/5 rounded-lg p-4 overflow-y-auto flex gap-4"
        style="scrollbar-gutter: stable;"
      >
        <div v-if="hasSticky" class="sticky top-0 z-10 w-[40%]">
          <slot name="sticky"></slot>
        </div>
        <div :class="{ 'w-[60%]' : hasSticky }">
          <slot></slot>
        </div>
      </div>
    </div>

    <div class="absolute inset-0 z-[-1] bg-gradient-to-tr from-white dark:from-zinc-800 to-primary-100"></div>
  </div>
</template>
