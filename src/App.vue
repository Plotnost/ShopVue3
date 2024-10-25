<!-- src/App.vue -->
<script setup lang="ts">
import { ref, computed, Ref } from 'vue';
import Catalog from './components/Catalog.vue';
import Cart from './components/Cart.vue';
import Product from './components/Product.vue';

// Типы для товара и корзины
interface Product {
  id: number;
  name: string;
  price: number;
}

// Определение маршрутов
const routes: Record<string, any> = {
  '/': Catalog,
  '/cart': Cart,
  '/product': Product,
};

// Текущий путь и компонент
const currentPath = ref(window.location.hash);
const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/'] || Catalog;
});

// Корзина и функции для управления
const cart: Ref<Product[]> = ref([]);
const addToCart = (product: Product) => {
  cart.value.push(product);
};
const removeFromCart = (productId: number) => {
  cart.value = cart.value.filter((item) => item.id !== productId);
};

// Слушатель события для изменения пути
window.addEventListener('hashchange', () => {
  currentPath.value = window.location.hash;
});
</script>

<template>
  <nav>
    <a href="#/">Каталог</a> |
    <a href="#/cart">Корзина</a>
  </nav>

  <component
    :is="currentView"
    :cart="cart"
    :add-to-cart="addToCart"
    :remove-from-cart="removeFromCart"
  />
</template>

<style scoped>
nav a {
  margin-right: 10px;
  text-decoration: none;
  color: #42b983;
}
</style>
