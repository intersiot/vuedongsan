<template>
  <div>
    <img :src="원룸.image" class="room-img" alt="room0.jpg">
    <h4>{{ 원룸.title }}</h4>
    <p>{{ 원룸.price }}원</p>
    <!-- <button @click="신고수[i]++">허위매물신고버튼</button> <span>신고수 : {{ 신고수[i] }}</span> -->
  </div>
</template>

<script>
export default {
  name: 'CardComponent',
  props: {
    원룸: Object,
  }
}
</script>

<style>
.room-img {
  width: 100%;
  margin-top: 40px;
}
</style>