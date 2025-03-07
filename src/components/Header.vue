<script setup lang="ts">
import { ref, onMounted, onUnmounted } from "vue";
import ThemeSelector from "./ui/ThemeSelector.vue";
import { Home, User, Briefcase, Folder, Mail } from "lucide-vue-next";

const menu = ref<HTMLElement | null>(null);
let ticking = false;

const handleScroll = () => {
  if (!ticking) {
    requestAnimationFrame(() => {
      if (!menu.value) return;

      const scrollPosition = window.scrollY || 0;

      if (scrollPosition >= 200) {
        menu.value.classList.add("border");
        menu.value.style.backgroundColor = "var(--header-color)";
        menu.value.style.borderColor = "var(--line-color)";
        menu.value.style.opacity = "0.9";
      } else {
        menu.value.classList.remove("border");
        menu.value.style.backgroundColor = "var(--header-color)";
        menu.value.style.opacity = "1";
      }

      ticking = false;
    });

    ticking = true;
  }
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
});
onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});

const navItems = [
  { name: "Inicio", icon: Home, href: "#inicio" },
  { name: "Sobre Mi", icon: User, href: "#sobremi" },
  { name: "Experiencia", icon: Briefcase, href: "#experiencia" },
  { name: "Proyectos", icon: Folder, href: "#proyectos" },
  { name: "Contacto", icon: Mail, href: "#contacto" },
];
</script>

<template>
  <header class="flex justify-center">
    <!-- NAV DESKTOP -->
    <nav class="fixed max-md:hidden pt-2 z-50">
      <ul
        ref="menu"
        class="flex flex-row justify-center p-3 gap-5 max-sm:text-sm header text-base rounded-full font-bold"
      >
        <li v-for="item in navItems" :key="item.name" class="hover:text-[var(--title-color)]">
          <a :href="item.href">{{ item.name }}</a>
        </li>
      </ul>
      <ThemeSelector />
    </nav>

    <div class="md:hidden fixed top-4 right-4 z-50 scale-50 sm:scale-100">
      <ThemeSelector />
    </div>
    <!-- NAV MOBILE -->
    <div class="fixed md:hidden z-50 w-full h-16 max-w-lg -translate-x-1/2 rounded-full bottom-4 left-1/2 header">
      <div class="grid h-full max-w-lg grid-cols-5 mx-auto">
        <button
          v-for="item in navItems"
          :key="item.name"
          type="button"
          class="inline-flex flex-col items-center justify-center px-5 hover:bg-gray-50 dark:hover:bg-gray-800 group"
        >
          <a :href="item.href" class="flex flex-col items-center gap-1">
            <component :is="item.icon" class="w-6 h-6 text-[var(--title-color)] stroke-[1.5]" />
            <span class="text-[10px] sm:text-xs text-[var(--title-color)] whitespace-nowrap">
              {{ item.name }}
            </span>
          </a>
        </button>
      </div>
    </div>
  </header>
</template>

