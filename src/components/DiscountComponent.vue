<template>
  <div class="discount">
    <h4>지금 결제하면 {{ amount }}% 할인!</h4>
  </div>  
</template>

<script>
export default {
    name: 'DiscountComponent',
    data() {
      return {
        amount: 30,
      }
    },
    mounted() { // App.vue가 mount되고 나서 안의 코드 실행해주셈
      setInterval(() => {
        if (this.amount > 0) {
          this.amount--;
        } else if (this.amount <= 0) {
          clearInterval // setInterval을 멈추는 함수
        }
      }, 1000)
    },
}
</script>

<style>
.discount {
  background: lightgray;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
</style>
