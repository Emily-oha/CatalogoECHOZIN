<template>
  <header class="border-b bg-white/80 backdrop-blur">
    <div class="mx-auto flex max-w-6xl items-center justify-between px-4 py-4">
      <div class="flex items-center gap-3">
        <div class="grid h-10 w-10 place-items-center rounded-2xl bg-black text-white font-bold">
        
        </div>
        <div>
          <h1 class="text-lg font-semibold leading-tight">Echozin Store</h1>
          <p class="text-sm text-gray-500 leading-tight">Catálogo simples</p>
        </div>
      </div>

      <div class="hidden sm:flex items-center gap-3">
        <input
          v-model="localQuery"
          @input="$emit('update:query', localQuery)"
          class="w-72 rounded-xl border px-3 py-2 text-sm outline-none focus:ring-2 focus:ring-black/20"
          type="text"
          placeholder="Buscar produto..."
        />
      </div>
    </div>

    <div class="sm:hidden px-4 pb-4">
      <input
        v-model="localQuery"
        @input="$emit('update:query', localQuery)"
        class="w-full rounded-xl border px-3 py-2 text-sm outline-none focus:ring-2 focus:ring-black/20"
        type="text"
        placeholder="Buscar produto..."
      />
    </div>
  </header>
</template>

<script setup>
import { ref, watch } from "vue";

const props = defineProps({
  query: { type: String, default: "" },
});

defineEmits(["update:query"]);

const localQuery = ref(props.query);

watch(
  () => props.query,
  (v) => {
    if (v !== localQuery.value) localQuery.value = v;
  }
);
</script>
