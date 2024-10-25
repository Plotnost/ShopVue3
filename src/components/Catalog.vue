<!-- src/Catalog.vue -->
<template>
  <div>
    <h2>Каталог товаров</h2>
    <ul>
      <li v-for="product in products" :key="product.id">
        {{ product.name }} - {{ product.price }} ₽
        <button @click="addToCart(product)">Добавить в корзину</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Catalog',
  props: {
    addToCart: Function, // Принимаем функцию для добавления в корзину как пропс
  },
  data() {
    return {
      products: [
        { id: 1, name: 'Товар 1', price: 100 },
        { id: 2, name: 'Товар 2', price: 200 },
        { id: 3, name: 'Товар 3', price: 300 },
      ],
    };
  },
};
</script>
