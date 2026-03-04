<template>
  <div class="min-h-screen bg-gray-50 text-gray-900">
    <AppHeader v-model:query="query" />

    <main class="mx-auto max-w-6xl px-4 py-8">
      <div class="flex items-center justify-between gap-4">
        <h2 class="text-xl font-semibold">Produtos</h2>

        <select
          v-model="selectedCategory"
          class="rounded-xl border bg-white px-3 py-2 text-sm outline-none focus:ring-2 focus:ring-black/20"
        >
          <option value="all">Todas as categorias</option>
          <option v-for="c in categories" :key="c" :value="c">{{ c }}</option>
        </select>
      </div>

      <p class="mt-2 text-sm text-gray-600">
        Mostrando <span class="font-medium">{{ filteredProducts.length }}</span> de
        <span class="font-medium">{{ products.length }}</span>
      </p>

      <div class="mt-6 grid gap-5 sm:grid-cols-2 lg:grid-cols-3">
        <ProductCard
          v-for="p in filteredProducts"
          :key="p.id"
          :product="p"
          @buy="handleBuy"
        />
      </div>

      <div
        v-if="filteredProducts.length === 0"
        class="mt-10 rounded-2xl border bg-white p-8 text-center text-gray-600"
      >
        Nenhum produto encontrado 😕
      </div>
    </main>

    <AppFooter />
  </div>
</template>

<script setup>
import { computed, ref } from "vue";
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";
import ProductCard from "./components/ProductCard.vue";

const query = ref("");
const selectedCategory = ref("all");

const products = ref([
  {
    id: 1,
    title: "Tênis esportivo",
    category: "Calçados",
    price: 199.9,
    description: "Conforto máximo para sua corrida e caminhada no dia a dia.",
    image:
      "https://images.unsplash.com/photo-1542291026-7eec264c27ff?q=80&w=1200&auto=format&fit=crop",
  },
  {
    id: 2,
    title: "Relógio Smart",
    category: "Acessórios",
    price: 250,
    description: "Monitora passos, batimentos e notificações do celular.",
    image:
      "https://images.unsplash.com/photo-1523275335684-37898b6baf30?q=80&w=1200&auto=format&fit=crop",
  },
  {
    id: 3,
    title: "Mochila Casual",
    category: "Bolsas",
    price: 139.9,
    description: "Espaçosa, resistente e perfeita para escola e trabalho.",
    image:
      "https://images.unsplash.com/photo-1553062407-98eeb64c6a62?q=80&w=1200&auto=format&fit=crop",
  },
  {
    id: 4,
    title: "Camiseta básica",
    category: "Roupas",
    price: 49.9,
    description: "Malha leve e confortável. Combine com tudo.",
    image: "",
  },
]);

const categories = computed(() => {
  const set = new Set(products.value.map((p) => p.category));
  return Array.from(set);
});

const filteredProducts = computed(() => {
  const q = query.value.trim().toLowerCase();
  return products.value.filter((p) => {
    const matchQuery =
      !q ||
      p.title.toLowerCase().includes(q) ||
      p.description.toLowerCase().includes(q) ||
      p.category.toLowerCase().includes(q);

    const matchCategory = selectedCategory.value === "all" || p.category === selectedCategory.value;

    return matchQuery && matchCategory;
  });
});

function handleBuy(product) {
  alert(`Você clicou em comprar: ${product.title}`);
}
</script>
