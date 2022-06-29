<template>
    <div class="black-bg" v-if="모달창열렸니 == true">
      <div class="white-bg">
        <img :src="원룸들[누른거].image" class="room-img" />
        <h4>{{ 원룸들[누른거].title }}</h4>
        <p>{{ 원룸들[누른거].content }}</p>
        <!-- <input @input="month = $event.target.value"> -->
        <input v-model="month">
        <p>{{ month }}개월 선택함: {{ 원룸들[누른거].price * month }}</p>
        <button v-on:click="close">닫기</button>
      </div>
  </div>
</template>

<script>
export default {
  name: 'ModalComponent',
  data() {
    return {
      month: 1,
    }
  },
  // 데이터감시
  watch: { // 함수식으로 작성하면 됨.
    month(param) {
      // 사용자가 month를 글자로 입력하면 경고문 띄워주셈.
      if (isNaN(param) == true) {
        alert('문자입력하지마세요.')
        this.month = 1
      } else if (param >= 13) {
        alert('12보다 큰 숫자 입력하지마세요.')
        this.month = 1
      }
    }
  },
  props: {
    원룸들: Array,
    누른거: Number,
    모달창열렸니: Boolean,
  },
  methods: {
    close() {
      this.$emit('closeModal')
    }
  },
  beforeUpdate() { // 업데이트 되기 전에
    if (this.month == 2) { // month라는 데이터를 검사 -> 데이터가 2면
      alert('2개월은 너무 적음') // 원하는 동작을 실행
      this.month = 3
    }
  },
}
</script>

<style>
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
.modal-close-btn {
  background: darkcyan;
  color: #fff;
  border: 0;
  border-radius: 5px;
  padding: 5px 20px;
  cursor: pointer;
}
</style>
