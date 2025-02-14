<template>
  <nav class="navbar">
    <ul class="nav-list">
      <li><router-link to="/main">Главная</router-link></li>
      <li><router-link to="/products">Каталог товаров</router-link></li>

      <li>
        <router-link to="/cart">
          Корзина
          <span v-if="cartItemCount" class="cart-count">{{ cartItemCount }}</span>
        </router-link>
      </li>
      <li><router-link to="/orders">Оформленные заказы</router-link></li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'Header',
  computed: {
    cartItemCount() {
      return this.$store.state.cart.reduce((total, item) => total + item.quantity, 0);
    }
  }
};
</script>

<style scoped>
.navbar {
  background-color: rgba(11, 156, 49, .2);
  padding: 10px;
}

.nav-list {
  list-style-type: none;
  display: flex;
  justify-content: space-around;
}

.nav-list li {
  color: white;
  text-decoration: none;
  padding: 10px;
  position: relative;
}

.nav-list li a {
  color: black;
  text-decoration: none;
  font-family: Bitter, sans-serif;
}

.nav-list li a:hover {
  color: black;
}

.cart-count {
  background-color: red;
  color: white;
  border-radius: 10%;
  padding: 4px 8px;
  font-size: 12px;
  min-width: 10px;
  text-align: center;
  position: absolute;
  right: -20px;
}
</style>