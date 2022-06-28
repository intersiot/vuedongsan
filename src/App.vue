<template>
  <!-- 모달창 -->
  <div class="black-bg" v-if="모달창열렸니 == true">
    <div class="white-bg">
      <img :src="원룸들[누른거].image" class="room-img" />
      <h4>{{ 원룸들[누른거].title }}</h4>
      <p>{{ 원룸들[누른거].content }}</p>
      <button v-on:click="모달창열렸니 = false">닫기</button>
    </div>
  </div>
  <!-- 메뉴 -->
  <div class="menu">
    <a v-for="(작명, i) in 메뉴들" :key="i">{{ 작명 }}</a>
  </div>
  <!-- 콘텐츠 -->
  <!-- <div v-for="(a, i) in products" :key="i">
    <h4>products[i]</h4>
    <p>50 만원</p>
  </div> -->
  <div v-for="(원룸, i) in 원룸들" :key="i">
    <img :src="원룸.image" class="room-img" alt="room0.jpg">
    <h4 @click="모달창열렸니 = true, 누른거 = i">{{ 원룸.title }}</h4>
    <p>{{ 원룸.price }}원</p>
    <!-- <button @click="신고수[i]++">허위매물신고버튼</button> <span>신고수 : {{ 신고수[i] }}</span> -->
  </div>
</template>

<!-- 
    동적인 UI 만드는 법
    1. HTML, CSS로 디자인 해두셈(기본)
    2. UI 현재 상태를 데이터로 저장해둠
    3. 데이터에 따라서 UI가 어떻게 보일지 작성함
   -->

<script>
import data from './assets/oneroom.js'

export default {
  name: 'App',
  // 데이터 보관함
  data () {
    return {
      // 여기에 데이터 보관하자.
      누른거: 0,
      원룸들: data,
      모달창열렸니: true, // true or false, 0 or 1
      신고수: [0, 0, 0],
      메뉴들: ['Home', 'Shop', 'About'],
      products: ['역삼동원룸', '천호동원룸', '망원동원룸'],
    }
  },
  methods: {
    // 함수만드는 공간
    increase() {
      this.신고수 += 1
    }
  },
  components: {
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%; height: 100%;
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

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: #fff;
  padding: 10px;
  text-decoration: none;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}

.modal-close-btn {
  background: darkcyan;
  color: #fff;
  border: 0;
  border-radius: 5px;
  padding: 5px 20px;
  cursor: pointer;
}
</style>
