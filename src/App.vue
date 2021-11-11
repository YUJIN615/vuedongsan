<template>
  <nav>
    <ul>
      <li v-for="menu in menus" :key="menu">
        <a href="">{{ menu }}</a>
      </li>
    </ul>
  </nav>

  <transition name="scale">
    <div class="discountBanner" v-if="showBanner">
      지금 구매하면 {{ discountPercent }}% 할인!
    </div>
  </transition>

  <div class="buttonGroup">
    <button @click="sortPrice">가격 낮은순</button>
    <button @click="sortPrice2">가격 높은순</button>
    <button @click="sortTitle">가나다순</button>
    <button @click="sortReturn">원래대로</button>
  </div>

  <product-card 
    :room="room"
    v-for="(room, i) in rooms" :key="i"
    @openModal="openModal(i)"
  ></product-card>

  <transition name="fade">
    <product-modal 
    :rooms="rooms"
    :selectedRoom="selectedRoom"
    v-if="modalState"
    @closeModal="closeModal"
    ></product-modal>
  </transition>


</template>

<script>
import roomsData from './roomsData'
import productCard from './components/productCard.vue'
import productModal from './components/productModal.vue'

export default {
  name: 'App',
  components: {
    productCard,
    productModal,
  },
  data() {
    return {
      menus: ['Home', 'About', 'Product', 'Mypage'],
      roomsOriginal: [...roomsData],
      rooms: [...roomsData],
      showBanner: true,
      discountPercent: 20,
      totalPrice: 0,
      modalState: false,
      selectedRoom: 0,
    }
  },
  methods: {
    openModal(i) {
      this.modalState = true;
      this.selectedRoom = i;
    },
    closeModal() {
      this.modalState = false;
    },
    sortPrice() {
      this.rooms.sort((a,b)=> {
        return a.price - b.price;
      })
    },
    sortPrice2() {
      this.rooms.sort((a,b)=> {
        return b.price - a.price;
      })
    },
    sortTitle() {
      this.rooms.sort((a,b) => {
        const nameA = a.title.toUpperCase();
        const nameB = b.title.toUpperCase();
        if(nameA < nameB) {
          return -1;
        }
        if (nameA > nameB) {
          return 1;
        }
        return 0;
      })
    },
    sortReturn() {
      this.rooms = [...this.roomsOriginal];
    }
  },
  mounted() {
    setInterval(() => {
      if (this.discountPercent > 0) {
        this.discountPercent--
        
        if (this.discountPercent === 0) {
          this.showBanner = false;
        }
      }
    }, 1000)
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  list-style: none;
  text-decoration: none;
  box-sizing: border-box
}
nav {
  max-width: 700px;
  background: rgb(85, 105, 216);
  border-radius: 8px;
  margin: 0 auto 30px;;
  padding: 0 30px;
}
nav ul {
  display: flex;
  justify-content: center;
}
nav ul li a {
  display: block;
  padding: 30px;
  color: #fff;
}

.discountBanner{
  width: 700px;
  padding: 40px;
  border-radius: 8px;
  margin: 0 auto 30px;
  background: #eee;
  text-align: center;
}

.buttonGroup {
  width: 700px;
  margin: 0 auto 20px;
}

.buttonGroup button {
  padding: 2px 7px;
  margin-right: 15px;
}

.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: all .5s;
}
.fade-enter-to {
  opacity: 1;
}
.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all .5s;
}
.fade-leave-to {
  opacity: 0;
}

.scale-leave-from {
  opacity: 1;
}
.scale-leave-active {
  transition: all 1.5s;
}
.scale-leave-to {
  opacity: 0;
  padding: 0;
  margin: 0 auto;
  height: 0;
}
</style>
