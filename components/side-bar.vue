<script setup lang="ts">
export interface Menu {
  id: string
  label: string
  url?: string
  icon: string
}

const menus: Menu[] = [
  { id: 'dashboard', label: 'Dashboard', url: '/dashboard', icon: 'i-material-symbols:dashboard-outline' },
  { id: 'create-quiz', label: 'Create Quiz', url: '/quiz/create', icon: 'i-material-symbols:quiz-outline' },
  { id: 'quizzes', label: 'My Quizzes', url: '/quiz', icon: 'i-material-symbols:list' },
  { id: 'question-bank', label: 'Question Bank', url: '/question-bank', icon: 'i-material-symbols:library-books-outline' },
  { id: 'reports-analytics', label: 'Reports & Analytics', url: '/reports-analytics', icon: 'i-material-symbols:insights' },
  { id: 'leaderboard', label: 'Leaderboard', url: '/leaderboard', icon: 'i-material-symbols:leaderboard-outline' },
]

const activeMenu = ref<string>('dashboard');
const setActiveMenu = (menuId: string) => {
  activeMenu.value = menuId;
}
</script>

<template>
  <div class="w-[250px] py-4 pl-2 pr-4">

    <div class="text-lg font-semibold px-3 mb-6 flex items-center justify-between">
      <div class="flex items-center gap-5">
        <UIcon name="i-material-symbols:lightbulb-2-outline" class="w-5 h-5" />
        Quizify
      </div>
    </div>

    <ul class="flex flex-col gap-1">
      <li
        v-for="menu in menus"
        :key="menu.id"
        class="flex items-center gap-5 px-3 py-2 rounded-md cursor-pointer"
        :class="activeMenu === menu.id ? 'bg-white/50' : 'hover:bg-white/50'"
        @click="setActiveMenu(menu.id)"
      >
        <UIcon :name="menu.icon" class="w-5 h-5" />
        {{ menu.label }}
      </li>
    </ul>

  </div>
</template>