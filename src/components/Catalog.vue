<template>
    <div>
      <h1>Каталог товаров</h1>
  
      <!-- Форма поиска -->
      <input
        type="text"
        v-model="searchQuery"
        placeholder="Поиск товаров..."
        class="search-input"
      />
  
      <!-- Список товаров -->
      <div class="product-list">
        <div v-for="product in filteredProducts" :key="product.id" class="product-item">
          <h3>{{ product.name }}</h3>
          <p>Цена: {{ product.price }} ₽</p>
          <button @click="addToCart(product)">Добавить в корзину</button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, computed } from 'vue';
  
  export default {
    name: 'ProductCatalog',
    setup() {
      // Массив товаров
      const products = ref([
        { id: 1, name: 'Товар 1', price: 100 },
        { id: 2, name: 'Товар 2', price: 200 },
        { id: 3, name: 'Товар 3', price: 300 },
        // Добавьте больше товаров по мере необходимости
      ]);
  
      // Переменная для хранения поискового запроса
      const searchQuery = ref('');
  
      // Фильтрация товаров по запросу
      const filteredProducts = computed(() =>
        products.value.filter((product) =>
          product.name.toLowerCase().includes(searchQuery.value.toLowerCase())
        )
      );
  
      // Функция добавления товара в корзину
      const addToCart = (product) => {
        console.log(`Товар добавлен в корзину: ${product.name}`);
        // Логика добавления в корзину
      };
  
      return {
        products,
        searchQuery,
        filteredProducts,
        addToCart,
      };
    },
  };
  </script>
  
  <style scoped>
  /* Стили для каталога */
  .search-input {
    margin-bottom: 1rem;
    padding: 0.5rem;
    width: 100%;
    box-sizing: border-box;
  }
  
  .product-list {
    display: flex;
    flex-wrap: wrap;
  }
  
  .product-item {
    border: 1px solid #ccc;
    padding: 1rem;
    margin: 0.5rem;
    width: calc(33.333% - 1rem);
    box-sizing: border-box;
  }
  </style>
  