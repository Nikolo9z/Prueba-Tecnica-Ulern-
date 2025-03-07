<script setup>
const props = defineProps({
  title: String,
  description: String,
  image: String,
  technologies: Array,
  links: Array
})
</script>

<template>
  <div class="grid grid-cols-2 max-md:grid-cols-1 gap-4 max-md:p-2 max-md:py-5">
    <h3 class="projectstitles font-semibold col-span-2 max-md:col-span-1">
      {{ title }}
    </h3>
    <img
      loading="lazy"
      class="col-span-1 row-span-3 rounded-lg w-full h-80 object-cover"
      :src="image"
      :alt="title"
    />

    <div class="flex flex-col gap-2 font-semibold">
      <p class="text-white text-base max-sm:text-sm">
  {{ description }}
</p>

      <h3 class="projectstitles pt-2">Tecnologías usadas</h3>
      <div class="flex gap-2 max-sm">
        <span
          v-for="tech in technologies"
          :key="tech.name"
          class="flex cursor-pointer relative px-0.5 justify-start items-center rounded-xl border-2 border-gray-950 overflow-hidden"
          :style="{ backgroundColor: tech.color + '30' }"
        >
          <img
            loading="lazy"
            class="size-6 mr-1"
            :src="tech.img"
            :alt="tech.name"
          />
          {{ tech.name }}
        </span>
      </div>

      <div class="flex gap-2 pt-2">
        <a
          v-for="link in links"
          :key="link.url"
          :href="link.url"
          target="_blank"
          rel="noopener noreferrer"
          class="bg-gray-900 max-sm:text-sm rounded-3xl px-5 py-1  cursor-pointer text-base border-2 border-[var(--projectstitles-color)] hover:bg-gray-800 transition"
        >
          {{ link.text }}
        </a>
      </div>
    </div>
  </div>
</template>
