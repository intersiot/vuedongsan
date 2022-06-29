<template>
  <!-- 모달창 -->
  <transition name="fade">
    <Modal @closeModal="모달창열렸니 = false" 
      v-bind:원룸들="원룸들" 
      :누른거="누른거" 
      :모달창열렸니="모달창열렸니" /> <!-- :원룸들="원룸들"로 써도 됨. -->
  </transition>
  <!-- 메뉴 -->
  <div class="menu">
    <a v-for="(작명, i) in 메뉴들" :key="i">{{ 작명 }}</a>
  </div>
  <!-- 홍보배너 -->
  <Discount v-if="showDiscount == true" />
  <!-- 정렬버튼 -->
  <button class="sortBtn" @click="spellingSort()">가나다순정렬</button>
  <button class="sortBtn" @click="priceSort()">가격순정렬</button>
  <button class="sortBtn" @click="priceReverseSort()">가격역순정렬</button>
  <button class="sortBtn" @click="PriceSearchSort()">50만원이하</button>
  <button class="sortBtn" @click="sortBack()">되돌리기</button>
  <!-- 콘텐츠 -->
  <!-- <Card :원룸="원룸들[0]" v-for="작명 in 반복할횟수/데이터" :key="" /> -->
  <Card @openModal="모달창열렸니 = true; 누른거 = $event" :원룸="원룸들[i]" v-for="(작명, i) in 원룸들" :key="작명" />
  <!-- 
    App.vue <Card />에 이렇게 해도 됨 : 이벤트 버블링 현상 때문에
    <Card @click="모달창열렸니 = true" :원룸="원룸들[i]" v-for="(작명, i) in 원룸들" :key="작명" />
   -->

  <!-- <Card :원룸="원룸들[0]" />
  <Card :원룸="원룸들[1]" />
  <Card :원룸="원룸들[2]" /> -->
  
  <!-- <div v-for="(a, i) in products" :key="i">
    <h4>products[i]</h4>
    <p>50 만원</p>
  </div> -->
  <!-- <div v-for="(원룸, i) in 원룸들" :key="i">
    <img :src="원룸.image" class="room-img" alt="room0.jpg">
    <h4 @click="모달창열렸니 = true, 누른거 = i">{{ 원룸.title }}</h4>
    <p>{{ 원룸.price }}원</p>
    <button @click="신고수[i]++">허위매물신고버튼</button> <span>신고수 : {{ 신고수[i] }}</span>
  </div> -->
</template>

<!-- 
    동적인 UI 만드는 법
    1. HTML, CSS로 디자인 해두셈(기본)
    2. UI 현재 상태를 데이터로 저장해둠
    3. 데이터에 따라서 UI가 어떻게 보일지 작성함
   -->

<script>
import data from './assets/oneroom.js'
import Discount from './components/DiscountComponent.vue'
import Modal from './components/ModalComponent.vue'
import Card from './components/CardComponent.vue'

export default {
  name: 'App',
  // 데이터 보관함
  data () {
    return {
      // 여기에 데이터 보관하자.
      showDiscount: true, // 현재 디스카운트의 상태
      원룸들오리지널: [...data], // 원래 데이터 필요할 때 사용
      // 별개의 사본을 만들려면 [...자료형]
      누른거: 0,
      원룸들: data,
      모달창열렸니: false, // true or false, 0 or 1
      신고수: [0, 0, 0],
      메뉴들: ['Home', 'Shop', 'About'],
      products: ['역삼동원룸', '천호동원룸', '망원동원룸'],
    }
  },
  methods: {
    // 함수만드는 공간
    increase() {
      this.신고수 += 1
    },
    spellingSort() {
      this.원룸들.sort(function(a, b) {
        let x = a.title.toLowerCase()
        let y = b.title.toLowerCase()

        if (x < y) {
          return -1
        } else if (x > y) {
          return 1
        }
        return 0
      })
    },
    priceSort() {
      this.원룸들.sort(function(a, b) {
        return a.price - b.price
      })
    },
    priceReverseSort() {
      this.원룸들.sort(function(a, b) {
        return b.price - a.price
      })
    },
    PriceSearchSort() {
      const searchPrice = 500000
      this.원룸들 = this.원룸들.filter(function(a) {
        return a.price <= searchPrice
      })
    },
    sortBack() {
      // this.원룸들 = this.원룸들오리지널
      this.원룸들 = [...this.원룸들오리지널]
    }
  },
  created() {
    // 서버에서 데이터 가져오는 코드
  },
  mounted() { // 마운트되고 나서
    // setTimeout(() => {
    //   this.showDiscount = false
    // }, 2000)
    setInterval(() => {
      if (this.$refs.discount.amount > 0) {
        this.$refs.discount.amount--
      } else if (this.$refs.discount.amount <= 0) { // 할인율이 0이되면 감소를 멈춤
        clearInterval
        this.showDiscount = false // 할인율이 0이되면 사라짐
      }
    }, 1000);
  },
  components: {
    Discount, // 작명 : 등록할컴포넌트 -> 이렇게 써도 됨
    Modal,
    Card,
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
/* 
.start {
  opacity: 0;
  transition: all 1;
}
.end {
  opacity: 1;
} */

/* 등장애니메이션 */
.fade-enter-from {
  /* 시작스타일 */
  opacity: 0;
}
.fade-enter-active {
  /* 트랜지션 */
  transition: all 1s;
}
.fade-enter-to {
  /* 끝날 때 스타일 */
  opacity: 1;
}

/* 퇴장애니메이션 */
.fade-leave-from {
  /* 시작스타일 */
  opacity: 1;
}
.fade-leave-active {
  /* 트랜지션 */
  transition: all 1s;
}
.fade-leave-to {
  /* 끝날 때 스타일 */
  opacity: 0;
}

.sortBtn {
  border-radius: 3px;
  margin: 3px;
  padding: 10px;
  border: 0;
  background: lightcoral;
  color: white;
  cursor: pointer;
  margin-top: 10px;
}
</style>
