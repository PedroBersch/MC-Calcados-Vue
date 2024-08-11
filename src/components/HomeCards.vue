<script setup>
import Card from "./Card.vue";
import { RouterLink } from "vue-router";
</script>

<template>
  <!-- Developers and Employers -->
  <section class="py-4">
    <div class="container-xl lg:container m-auto">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4 p-4 rounded-lg">
        <Card>
          <h2 class="text-2xl font-bold">Para Clientes</h2>
          <p class="mt-2 mb-4">Ache os melhor preços aqui!</p>
          <RouterLink
            to="/products"
            class="inline-block bg-black text-white rounded-lg px-4 py-2 hover:bg-gray-700"
          >
            Procurar Produtos
          </RouterLink>
        </Card>
        <Card bg="bg-green-100">
          <h2 class="text-2xl font-bold">Para Funcionarios</h2>
          <p class="mt-2 mb-4">
            Lista de produtos para monitoramento do Estoque.
          </p>
          <RouterLink
            to="/products/add"
            class="inline-block bg-green-500 text-white rounded-lg px-4 py-2 hover:bg-green-600"
          >
            Adicionar Produto
          </RouterLink>
        </Card>
      </div>
    </div>
  </section>
</template>
