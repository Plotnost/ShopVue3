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

// Определяем, какой компонент отображать в зависимости от пути
const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/'] || Catalog; // возвращаем Catalog по умолчанию
});
</script>

<template>
  <nav>
    <a href="#/">Каталог</a> |
    <a href="#/cart">Корзина</a> |
    <a href="#/product">Карточка товара</a>
  </nav>

  <!-- Динамическое отображение компонента -->
  <component :is="currentView" />
</template>

<style scoped>
/* Пример стилей */
nav a {
  margin-right: 10px;
  text-decoration: none;
  color: #42b983;
}
</style>
