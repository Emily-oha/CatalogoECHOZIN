<template>
  <article class="overflow-hidden rounded-2xl border bg-white shadow-sm">
    <div class="aspect-[4/3] w-full bg-gray-100">
      <img
        v-if="product.image"
        :src="product.image"
        :alt="product.title"
        class="h-full w-full object-cover"
      />
      <div v-else class="grid h-full place-items-center text-sm text-gray-500">
        Sem imagem
      </div>
    </div>

    <div class="p-4">
      <div class="flex items-start justify-between gap-3">
        <h3 class="text-base font-semibold leading-snug">{{ product.title }}</h3>
        <span class="shrink-0 rounded-xl bg-gray-100 px-2.5 py-1 text-xs font-medium text-gray-700">
          {{ product.category }}
        </span>
      </div>

      <p class="mt-2 text-sm text-gray-600 line-clamp-2">
        {{ product.description }}
      </p>

      <div class="mt-4 flex items-center justify-between">
        <p class="text-lg font-semibold">
          {{ formatBRL(product.price) }}
        </p>

        <button
          class="rounded-xl bg-black px-3.5 py-2 text-sm font-medium text-white hover:opacity-90"
          @click="$emit('buy', product)"
        >
          Comprar
        </button>
      </div>
    </div>
  </article>
</template>

<script setup>
defineProps({
  product: {
    type: Object,
    required: true,
  },
});

defineEmits(["buy"]);

function formatBRL(value) {
  return new Intl.NumberFormat("pt-BR", { style: "currency", currency: "BRL" }).format(value);
}
</script>

<style scoped>
/* só para cortar o texto em 2 linhas com tailwind-like */
.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>
