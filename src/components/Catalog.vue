<!-- src/Catalog.vue -->
<template>
  <div>
    <h2>Каталог товаров</h2>
    <div class="product-list">
      <div v-for="product in products" :key="product.id" class="product-card">
        <img src="./image.png">
        <a href="#/product"class="product-name">{{ product.name }}</a>
        <p class="product-price">{{ product.price }} ₽</p>
        <button @click="addToCart(product)" class="add-to-cart-button">
          Добавить в корзину
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';


interface Product {
  id: number;
  name: string;
  price: number;
}

export default defineComponent({
  name: 'Catalog',
  props: {
    addToCart: Function as () => (product: Product) => void,
  },
  data() {
    return {
      products: [
        { id: 1, name: 'Товар 1', price: 100 },
        { id: 2, name: 'Товар 2', price: 200 },
        { id: 3, name: 'Товар 3', price: 300 },
      ] as Product[],
    };
  },
});
</script>

<style scoped>
/* Оформление списка товаров */
.product-list {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
}

/* Оформление карточек товаров */
.product-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 16px;
  height: 300px;
  width: 200px;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: transform 0.2s ease;
  background-color: #fff;
}

.product-card img{
  height: 50%;
  width: 80%;
  border: 1px solid #000;
  border-radius: 10px;
}

.product-card:hover {
  transform: scale(1.05);
}

/* Оформление названия товара */
.product-name {
  font-size: 18px;
  margin: 10px 0;
  text-align: center;
}

/* Оформление цены товара */
.product-price {
  font-size: 16px;
  color: #42b983;
  font-weight: bold;
}

/* Оформление кнопки добавления в корзину */
.add-to-cart-button {
  background-color: #42b983;
  color: #fff;
  border: none;
  border-radius: 4px;
  padding: 8px 16px;
  cursor: pointer;
  transition: background-color 0.2s ease;
  font-size: 14px;
}

.add-to-cart-button:hover {
  background-color: #369d6d;
}
</style>
