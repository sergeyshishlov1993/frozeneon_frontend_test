<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount, computed } from "vue";
import ProductCard from "../components/Block/ProductCard.vue";
import UiInput from "../components/Ui/UiInput.vue";

interface Product {
  id: number;
  title: string;
  description: string;
  price: number;
  category: string;
  discountPercentage: number;
  rating: number;
  brand: string;
  thumbnail: string;
}
interface ApiResponse {
  products: Product[];
}

const allProducts = ref<Product[]>([]);
const currentPage = ref<number>(0);
const isLoading = ref<boolean>(false);
const itemsPerPage = 10;
const isInitialized = ref<boolean>(false);
const searchQuery = ref<string>("");
const visibleProducts = ref<Product[]>([]);

const fetchAllProducts = async () => {
  const response = await fetch("https://dummyjson.com/products?limit=100");
  const data = (await response.json()) as ApiResponse;
  if (!data.products || !Array.isArray(data.products)) {
    throw new Error("API data is not valid");
  }
  allProducts.value = data.products;
  isInitialized.value = true;
};
const fetchNextProducts = (): void => {
  if (isLoading.value) return;
  if (currentPage.value * itemsPerPage >= allProducts.value.length) return;

  isLoading.value = true;

  const start = currentPage.value * itemsPerPage;
  const end = start + itemsPerPage;
  visibleProducts.value = [
    ...visibleProducts.value,
    ...allProducts.value.slice(start, end),
  ];
  currentPage.value++;
  isLoading.value = false;
};
const handleScroll = (): void => {
  const scrollPosition = window.innerHeight + window.scrollY;
  const bottomPosition = document.documentElement.offsetHeight;

  if (scrollPosition >= bottomPosition - 100) {
    fetchNextProducts();
  }
};
const search = (event: Event) => {
  const input = event.target as HTMLInputElement;
  searchQuery.value = input.value;
};

const filteredProducts = computed<Product[]>(() => {
  if (!searchQuery.value) {
    return visibleProducts.value;
  }

  return allProducts.value.filter((product) =>
    product.title.toLowerCase().includes(searchQuery.value.toLowerCase())
  );
});

onMounted(async () => {
  await fetchAllProducts();
  fetchNextProducts();
  window.addEventListener("scroll", handleScroll);
});

onBeforeUnmount(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>

<template>
  <div class="main-page" v-if="isInitialized">
    <UiInput
      type="search"
      placeholder="search"
      :value="searchQuery"
      @input="search"
    />

    <transition name="fade">
      <div v-if="!isLoading" class="products__wrapper is-loading">
        <ProductCard
          v-for="product in filteredProducts"
          :key="product.id"
          :product="product"
        />
      </div>
    </transition>

    <div v-if="!isLoading && filteredProducts.length === 0" class="not-found">
      <h2>Product Not Found</h2>
      <p>
        We couldn't find any products matching your search. Try another query.
      </p>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.main-page {
  padding-top: 50px;
  display: flex;
  flex-direction: column;
  gap: 40px;
  width: 100%;
}
.products__wrapper {
  display: flex;
  flex-direction: column;
  gap: 10px;
  opacity: 1;
  transition: opacity 0.5s ease-in-out;
}

.not-found {
  text-align: center;
  padding: 40px;
  border-radius: 12px;
  background-color: #f9f9f9;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  animation: fadeIn 0.5s ease-in-out;

  h2 {
    font-size: 24px;
    font-weight: bold;
    color: #333;
    margin-bottom: 10px;
  }

  p {
    font-size: 16px;
    color: #666;
    line-height: 1.5;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease-in-out, transform 0.3s ease-in-out;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

.fade-enter-to,
.fade-leave-from {
  opacity: 1;
  transform: translateY(0);
}
</style>
