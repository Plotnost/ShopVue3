<!-- src/App.vue -->
<script setup>
import { ref, computed } from 'vue';
import Catalog from './components/Catalog.vue';
import Cart from './components/Cart.vue';
import Product from './components/Product.vue';

// Определяем маршруты
const routes = {
  '/': Catalog,
  '/cart': Cart,
  '/product': Product,
};

// Отслеживание текущего пути
const currentPath = ref(window.location.hash);

// Обновление пути при изменении хэша
window.addEventListener('hashchange', () => {
  currentPath.value = window.location.hash;
});

// Определяем текущий компонент
const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/'] || Catalog;
});

// Состояние корзины
const cart = ref([]);

// Функция для добавления товара в корзину
const addToCart = (product) => {
  cart.value.push(product);
};

// Функция для удаления товара из корзины
const removeFromCart = (productId) => {
  cart.value = cart.value.filter((item) => item.id !== productId);
};
</script>

<template>
  <nav>
    <a href="#/">Каталог</a> |
    <a href="#/cart">Корзина</a> |
    <a href="#/product">Карточка товара</a>
  </nav>

  <!-- Динамическое отображение компонента с передачей состояния корзины -->
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
