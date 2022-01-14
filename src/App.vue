<template>
  <div id="app">
    <div class="black-bg" v-if="모달창열렸니 == true">
      <div class="white-bg">
        <h4>상세페이지</h4>
        <p>상세페이지 내용임</p>
        <button class="close_x" @click="모달창열렸니 = false">X</button>
      </div>
    </div>

    <div class="menu">
      <a v-for="a in 메뉴들" :key="a"> {{ a }}</a>
    </div>

    <div>
      <img src="./assets/room0.jpg" class="room-img" />
      <h4>{{ 원룸들[0] }}</h4>
      <p>50만원</p>
    </div>

    <div v-for="(prod, idx) in products" :key="prod">
      <img :src="imageUrl(idx)" class="room-img" />
      <h4 @click="모달창열렸니 = true">{{ prod }}</h4>
      <p>50만원</p>
      <button @click="increase(idx)">허위매물신고</button>
      <span> 신고수 : {{ 신고수[idx] }} </span>
    </div>
  </div>
</template>

<script>
import data from "./assets/room.js";

export default {
  name: "App",
  data() {
    return {
      원룸들: data,
      모달창열렸니: false,
      신고수: [0, 0, 0],
      메뉴들: ["Home", "Shop", "About"],
      products: ["역삼동원룸", "천호동원룸", "마포구원룸"],
    };
  },
  methods: {
    increase(idx) {
      this.신고수 = this.신고수.map((e, i) => (i == idx ? ++e : e));
    },
    imageUrl(idx) {
      return require(`./assets/room${idx}.jpg`);
    }
  },
  components: {},
};
</script>

<style>
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
  position: relative;
}

.white-bg .close_x {
  position: absolute;
  right: 20px;
  top: 20px;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}

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
</style>
