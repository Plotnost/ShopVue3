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

<script>
export default {
  name: 'Cart',
  props: {
    cart: Array, // Пропс для получения товаров в корзине
    removeFromCart: Function, // Пропс для функции удаления
  },
};
</script>
