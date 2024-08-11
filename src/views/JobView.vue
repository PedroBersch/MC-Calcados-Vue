<script setup>
import PulseLoader from "vue-spinner/src/PulseLoader.vue";
import axios from "axios";
import { reactive, onMounted } from "vue";
import { useRoute, RouterLink, useRouter } from "vue-router";
import BackButton from "@/components/BackButton.vue";
import { useToast } from "vue-toastification";

const route = useRoute();
const router = useRouter();
const toast = useToast();
const productId = route.params.id;

const state = reactive({
  product: {},
  isLoading: true,
});

const deleteProduct = async () => {
  try {
    await axios.delete(`/api/products/${productId}`);
    toast.success("products deleted Successfully");
    router.push("/products");
  } catch (error) {
    console.error("Error deleting products", error);
    toast.error("products Not deleted");
  }
};

onMounted(async () => {
  try {
    const response = await axios.get(`/api/products/${productId}`);
    state.product = response.data;
  } catch (error) {
    console.error("Error fetching products");
  } finally {
    state.isLoading = false;
  }
});
</script>
<template>
  <BackButton />
  <section v-if="!state.isLoading" class="bg-green-50">
    <div class="container m-auto py-10 px-6">
      <div class="grid grid-cols-1 md:grid-cols-70/30 w-full gap-6">
        <main>
          <div
            class="bg-white p-6 rounded-lg shadow-md text-center md:text-left"
          >
            <div class="text-gray-500 mb-4">{{ state.product.type }}</div>
            <h1 class="text-3xl font-bold mb-4">{{ state.product.title }}</h1>
            <div
              class="text-gray-500 mb-4 flex align-middle justify-center md:justify-start"
            >
              <i class="pi pi-map-marker mr-1 text-orange-500"></i>

              <p class="text-orange-700">{{ state.product.location }}</p>
            </div>
          </div>

          <div class="bg-white p-6 rounded-lg shadow-md mt-6">
            <h3 class="text-green-800 text-lg font-bold mb-6">
              products Description
            </h3>

            <p class="mb-4">
              {{ state.product.description }}
            </p>

            <h3 class="text-green-800 text-lg font-bold mb-2">Price</h3>

            <p class="mb-4">{{ state.product.price }}</p>
          </div>
        </main>

        <!-- Sidebar -->
        <aside>
          <!-- Company Info -->
          <div class="bg-white p-6 rounded-lg shadow-md">
            <h3 class="text-xl font-bold mb-6">Company Info</h3>

            <h2 class="text-2xl">{{ state.product.company.name }}</h2>

            <p class="my-2">
              {{ state.product.company.description }}
            </p>

            <hr class="my-4" />

            <h3 class="text-xl">Contact Email:</h3>

            <p class="my-2 bg-green-100 p-2 font-bold">
              {{ state.product.company.contactEmail }}
            </p>

            <h3 class="text-xl">Contact Phone:</h3>

            <p class="my-2 bg-green-100 p-2 font-bold">
              {{ state.product.company.contactPhone }}
            </p>
          </div>

          <!-- Manage -->
          <div class="bg-white p-6 rounded-lg shadow-md mt-6">
            <h3 class="text-xl font-bold mb-6">Manage products</h3>
            <RouterLink
              :to="`/products/edit/${state.product.id}`"
              class="bg-green-500 hover:bg-green-600 text-white text-center font-bold py-2 px-4 rounded-full w-full focus:outline-none focus:shadow-outline mt-4 block"
              >Edit products</RouterLink
            >
            <button
              @click="deleteProduct"
              class="bg-red-500 hover:bg-red-600 text-white font-bold py-2 px-4 rounded-full w-full focus:outline-none focus:shadow-outline mt-4 block"
            >
              Delete products
            </button>
          </div>
        </aside>
      </div>
    </div>
  </section>
  <div v-else class="text-center text-gray-500 py-6">
    <PulseLoader />
  </div>
</template>
