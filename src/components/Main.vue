<template>
  <div class="home">
    <div class="hero-section">

      <div class="welcome-text">
        <h1>Добро пожаловать в магазин Dominus Nox</h1>
        <p>
          Здесь вас ожидают товары первого класса. Что означает высокое качество продукции!
        </p>
        <router-link to="/products" class="shop-now-button">За покупками</router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
};
</script>

<style scoped>
.home {
  text-align: center;
}

.hero-section {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 50px 20px;
  background-color: #f9f9f9;
}

.hero-image {
  max-width: 100%;
  height: auto;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.welcome-text {
  margin-top: 20px;
  max-width: 600px;
  text-align: center;
}

.welcome-text h1 {
  font-size: 36px;
  margin-bottom: 20px;
  color: #333;
}

.welcome-text p {
  font-size: 18px;
  line-height: 1.6;
  color: #555;
}

.shop-now-button {
  display: inline-block;
  background-color:rgba(11, 156, 49, .2);
  color: black;
  padding: 10px 20px;
  font-size: 16px;
  text-decoration: none;
  border-radius: 5px;
  transition: background-color 0.3s ease;
}

.shop-now-button:hover {
  background-color: pink;
}
</style>