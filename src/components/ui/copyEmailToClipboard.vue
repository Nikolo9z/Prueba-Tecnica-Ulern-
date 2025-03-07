<script setup>
const email = "sanchez.nicolas.9917@gmail.com";

const copyToClipboard = async () => {
  await navigator.clipboard.writeText(email);
};
</script>

<template>
  <button class="cursor-pointer" aria-label='copiar Correo' @click="copyToClipboard">
    <slot></slot>
  </button>
</template>
