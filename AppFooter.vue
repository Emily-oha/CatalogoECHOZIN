<template>
  <footer class="mt-10 border-t bg-white">
    <div class="mx-auto max-w-6xl px-4 py-6 text-sm text-gray-600">
      <div class="flex flex-col gap-2 sm:flex-row sm:items-center sm:justify-between">
        <p>© {{ year }} Echozin Store — feito com Vue + Tailwind.</p>
        <p class="text-gray-500">Teste rápido de catálogo</p>
      </div>
    </div>
  </footer>
</template>

<script setup>
const year = new Date().getFullYear();
</script>
