<template>
  <div class="orders">
    <h2>Оформленные заказы</h2>
    <router-link to="/home" class="back-button">Назад</router-link>
    <div v-if="orders.length === 0" class="empty-orders">
      У вас пока нет оформленных заказов.
    </div>
    <div v-else>
      <div v-for="(order, index) in orders" :key="index" class="order-item">
        <h3>Заказ #{{ index + 1 }}</h3>
        <ul>
          <li v-for="item in order.items" :key="item.id" class="order-product">
            <span>{{ item.name }} ({{ item.quantity }} шт.) - {{ item.price * item.quantity }} ₽</span>
          </li>
        </ul>
        <p><strong>Итого: {{ order.total }} ₽</strong></p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    orders() {
      return this.$store.state.orders;
    }
  },
  methods: {
    goBack() {
      this.$router.push('/');
    }
  }
};
</script>

<style scoped>
.orders {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.back-button {
  background-color: rgba(11, 156, 49, .2);
  text-decoration: none;
  color: black;
  border: none;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  border-radius: 5px;

}

.back-button:hover {
  background-color: pink;
}

.empty-orders {
  margin-top: 20px;
  font-size: 18px;
  color: gray;
  text-align: center;
}

.order-item {
  border: 1px solid #ccc;
  padding: 15px;
  margin-bottom: 15px;
  border-radius: 5px;
}

.order-product {
  list-style-type: none;
  margin: 5px 0;
}

.order-product span {
  display: block;
  font-size: 14px;
}
.orders button{
  font-family: Garamond, sans-serif;
}
</style>