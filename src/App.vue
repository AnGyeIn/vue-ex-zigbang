<template>
  <div class="menu">
    <a v-for="(menu, index) in menus" :key="`menu-${index}`">{{ menu }}</a>
  </div>

  <div class="black-bg" v-if="isModalOpen">
    <div class="white-bg">
      <h4>상세페이지임</h4>
      <p>상세페이지 내용임</p>
      <button @click="isModalOpen = false">닫기</button>
    </div>
  </div>

  <div
    v-for="({ id, title, image, content, price }, index) in products"
    :key="`product-${id}`"
  >
    <!-- <img :src="require(`@/assets/room${index}.jpg`)" class="room-img" /> -->
    <img :src="image" class="room-img" />
    <h4 @click="isModalOpen = true">{{ title }}</h4>
    <h4>{{ content }}</h4>
    <p>{{ price }}원</p>
    <button @click="report(index)">허위매물신고</button>
    <span>신고수 : {{ reportsCounts[index] }}</span>
  </div>
</template>

<script>
import products from "./assets/oneroom";

export default {
  name: "App",
  data() {
    return {
      menus: ["Home", "Products", "About"],
      products,
      reportsCounts: products.map(() => 0),
      isModalOpen: false,
    };
  },
  methods: {
    report(index) {
      this.reportsCounts[index]++;
    },
  },
  components: {},
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}

body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}
.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}
</style>
