<script setup>
import { getProducts } from "../api/products";
</script>

<script>
export default {
  name: "ProductManager",
  data() {
    return {
      products: [],
    };
  },
  methods: {
    async loadProducts() {
      this.products = await getProducts();
    },
  },
  mounted() {
    this.loadProducts();
  },
};
</script>

<template>
  <main class="flex justify-center items-center flex-col min-h-screen">
    <h1 class="text-3xl">Termékek kezelése</h1>

    <table class="flex flex-col w-full p-4">
      <thead>
        <tr class="w-full flex justify-between">
          <th class="w-full text-left">azonosító</th>
          <th class="w-full text-left">név</th>
          <th class="w-full text-left">ár</th>
          <th class="w-full text-left">raktáron</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="product in products"
          :key="product.id"
          class="w-full flex justify-between my-2"
        >
          <td class="w-full text-left">{{ product.id }}</td>
          <td class="w-full text-left">{{ product.name }}</td>
          <td class="w-full text-left">{{ product.price }} Ft</td>
          <td class="w-full text-left">
            {{ product.inStock ? "Igen" : "Nem" }}
          </td>
        </tr>
      </tbody>
    </table>
  </main>
</template>
