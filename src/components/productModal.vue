<template>
  <div class="modal bg-black">
    <div class="bg-white">
      <img :src=rooms[selectedRoom].image alt="">
      <h4>{{ rooms[selectedRoom].title }}</h4>
      <p>{{ rooms[selectedRoom].content }}</p>
      <p class="price">월 {{ rooms[selectedRoom].price }}원 * <input type="text" v-model="month">개월 임대</p>
      <p>총 금액: {{ rooms[selectedRoom].price * month }}원</p>
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'productMdoal',
  props: {
    rooms: Array,
    selectedRoom: Number,
  },
  data() {
    return {      
      month: 1,
    }
  },
  watch: {
    month(a) {
      if (a == 2) {
        alert('임대는 3개월 이상부터 가능합니다');
        this.month = 3;
      }
      if (isNaN(a)) {
        alert('숫자를 입력하세요');
        this.month = 1;
      }
    }
  }
}
</script>

<style>
.modal.bg-black {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.3);
}
.modal .bg-white {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border-radius: 10px;
  max-width: 600px;
  height: auto;
  background: #fff;
  padding: 30px;
  text-align: center;
}
@media screen and (max-width: 768px) {
  .modal .bg-white {
    width: calc(100% - 60px);
  }
}
.modal .bg-white img {
  width: 100%;
}
.modal .bg-white h4 {
  margin: 20px 0;
}
.modal .bg-white p {
  margin-bottom: 16px;
}
.modal .bg-white p input {
  width: 100px;
  vertical-align: bottom;
}
.modal .bg-white button {
  padding: 2px 10px;
  margin-top: 10px
}
</style>