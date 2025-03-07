<script setup lang="ts">
import { ref, onMounted } from 'vue';

const themes = [
  { id: 'theme-1', name: 'Tema 1', colors: ['#1E034B', '#DDDF00'] },
  { id: 'theme-2', name: 'Tema 2', colors: ['#ee6c4d', '#293241'] }, 
  { id: 'theme-3', name: 'Tema 3', colors: ['#5e6472', '#aed9e0'] }, 
];

const selectedTheme = ref(themes[0].id);

const changeTheme = (themeId: string) => {
  selectedTheme.value = themeId;
  document.documentElement.setAttribute('data-theme', themeId);
  localStorage.setItem('theme', themeId);
};

onMounted(() => {
  const savedTheme = localStorage.getItem('theme') || themes[0].id;
  changeTheme(savedTheme);
});
</script>

<template>
<div class="fixed top-4 right-4 z-50 flex gap-2 items-center" role="radiogroup">
  <h3>Temas</h3>
  <button
    v-for="theme in themes"
    :key="theme.id"
    @click="changeTheme(theme.id)"
    class="w-10 h-10 rounded-full overflow-hidden border-2 border-gray-300 hover:border-gray-500 focus:outline-none focus:ring-2 cursor-pointer focus:ring-offset-2 focus:ring-indigo-500"
    :class="{ 'ring-2 ring-offset-2 ring-indigo-500': selectedTheme === theme.id }"
    :style="{
      background: `conic-gradient(${theme.colors[0]} 50%, ${theme.colors[1]} 50%)`,
    }"
    :title="theme.name"
    role="radio"
    :aria-checked="selectedTheme === theme.id"
  >
    <span class="sr-only">{{ theme.name }}</span>
  </button>
</div>

</template>