<!-- src/Cart.vue -->
<template>
  <div>
    <h2>Корзина</h2>
    <ul>
      <li v-for="item in cart" :key="item.id">
        {{ item.name }} - {{ item.price }} ₽
        <button @click="removeFromCart(item.id)">Удалить</button>
      </li>
    </ul>
    <p v-if="cart.length === 0">Корзина пуста</p>
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
  name: 'Cart',
  props: {
    cart: Array as () => Product[], // Пропс для товаров в корзине
    removeFromCart: Function as () => (productId: number) => void, // Функция удаления
  },
});
</script>
