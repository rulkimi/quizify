<template>
  <div class="h-screen">
    <div class="flex p-2 h-full">
      <SideBar />
      <div class="flex-grow bg-white shadow-lg dark:bg-white/5 rounded-lg p-4">
        <slot></slot>
      </div>
    </div>

    <div class="absolute inset-0 z-[-1] bg-gradient-to-tr from-white dark:from-zinc-800 to-primary-100"></div>
  </div>
</template>
