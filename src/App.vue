<script setup>
import { ref } from "vue";
import roomData from "./assets/js/room.js"; // export default 이므로 중괄호 없음

const Hotel = ref(roomData);
const sinGo = ref(Array(roomData.length).fill(0)); // 상품 개수만큼 0으로 채운 신고 수 배열
const modalOpen = ref(false);
const choice = ref(0); // 클릭한 상품 번호
const nav = ref(["호텔", "항공권", "렌터카"]);
</script>

<template>
  <!-- 모달창 -->
  <div class="black_bg" v-if="modalOpen">
    <div class="white_bg">
      <h4>{{ Hotel[choice].title }}</h4>
      <p>{{ Hotel[choice].content }}</p>
      <p>{{ Hotel[choice].price }}원</p>
      <button @click="modalOpen = false">닫기</button>
    </div>
  </div>

  <img alt="logo" src="./assets/logo.png" />

  <!-- 메뉴 -->
  <div class="menu">
    <a href="#" v-for="menu in nav" :key="menu">{{ menu }}</a>
  </div>

  <!-- 상품 5개를 반복문으로 진열 -->
  <div v-for="(room, i) in Hotel" :key="room.id">
    <img :src="room.image" class="imgS" alt="" />
    <h4
      @click="
        modalOpen = true;
        choice = i;
      "
    >
      {{ room.title }}
    </h4>
    <p>{{ room.price }}</p>
    <button @click="sinGo[i]++">허위매물신고</button>
    <span>{{ sinGo[i] }}</span>
  </div>
</template>

<style>
/* 모달창 디자인 */
body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
.black_bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
  top: 0;
  left: 0;
}
.white_bg {
  width: 100%;
  background: #fff;
  border-radius: 8px;
  padding: 20px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.menu {
  background: rgb(95, 49, 14);
  border-radius: 5px;
  padding: 15px;
}
.menu a {
  padding: 10px;
  color: white;
}
.imgS {
  width: 100%;
  margin-top: 50px;
}
</style>
