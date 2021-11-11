<template>
  <div class="productCard">
    <img :src=room.image alt="">
    <h4 @click="$emit('openModal')">{{ room.title }}</h4>
    <p>월 {{ room.price }}원</p>
  </div>
</template>

<script>
export default {
  name: 'productCard',
  props: {
    room: Object,
  }
}
</script>

<style>
.productCard {
  max-width: 700px;
  margin: 0 auto;
}
.productCard img {
  width: 100%;
}
.productCard h4 {
  font-size: 20px;
  text-align: center;
  margin: 20px 0;
  cursor: pointer;
}
.productCard p {
  text-align: center;
}
.productCard + .productCard {
  margin-top: 80px;
}
</style>