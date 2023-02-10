<template>

  <!--Header-->
  <div class="menu">
    <a v-for="item in items" :key="item">{{item}}</a>
  </div>
  
  <DiscountBanner v-if="showDiscount == true" :amount="amount"/>
  
  <button @click="priceLowSort">가격 낮은순 정렬</button>
  <button @click="price50Sort">가격 50만원 미만</button>
  <button @click="priceHighSort">가격 높은순 정렬</button>
  <button @click="titleSort">가나다 순 정렬</button>
  <button @click="sortBack">되돌리기</button>
  

  <transition name="fade">
  <ModalPopup @modalPopupClose="modal = false" :data="data" :clickCheck="clickCheck" :modal ="modal"/>
  </transition>

  <CardWindow @openModal="modal = true; clickCheck =$event" :data="data[i]" v-for="(datas , i) in data" :key="datas"  /> 
  

  <DiscountBanner v-if="showDiscount == true" :amount="amount"/>

</template>

<script>

import oneroomdata from './assets/oneroom.js';
import DiscountBanner from './DiscountBanner.vue';  
import ModalPopup from './ModalPopup.vue';
import CardWindow from './CardWindow.vue';



export default {
  name: 'App',
  data(){
    return{
       amount : 30,
       showDiscount : true,
       oneroomdataOriginal : [...oneroomdata],
       Object : {name : 'kim' , age :'20'},
       clickCheck : 0,    /*누른거*/ 
       data : oneroomdata,/*원룸List */
       modal : false,     /*모달창 */
       count : [0,0,0,0,0,0],/*신고수 */
       items : ['Home' , 'Shop' , 'About'],/*메뉴들 */
       products : ['역삼동원룸', '천호동원룸' , '마포구원룸'],
    }
  },
  
  methods : {
    increase(){
      this.count ++;
    },
    priceLowSort(){
      this.data.sort(function(a,b){
        return a.price - b.price
      })
    },
    priceHighSort(){
      this.data.sort(function(a,b){
        return b.price - a.price
      })
    },
    sortBack(){
    this.data =[...this.oneroomdataOriginal]; 
    },
    titleSort(){
      this.data = [...this.oneroomdataOriginal].sort((a,b) => {
        if(a.title < b.title) return -1;
        else if(b.title > a.title) return 0;
        else return 1;
      })
    },
    price50Sort : function(){
        this.data = this.data.filter(function(a){
        return a.price < '500000';
      });
    },
  },

  mounted(){
    setInterval(() => {
        this.amount --;
    }, 1000);
    setTimeout(() =>{
        this.showDiscount = false;
    } , 30000);
  },
  components: {
    DiscountBanner : DiscountBanner,
    ModalPopup : ModalPopup,
    CardWindow : CardWindow,
  }
}
</script>

<style>

.fade-enter-from {
  transform: translateY(-1000px);
} 
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  transform: translateY(0);
}

.fade-leave-from {
  opacity: 1;
} 
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0;
}

.start{
  opacity: 0;
  transition: all 2s;
}
.end{
  opacity: 1;
}

body{
  margin : 0
}
div{
  box-sizing: border-box;
}
.discount{
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
.black-bg{
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0, 5);
  position: fixed; padding: 20px;
}
.white-bg{
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
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
  padding :10px;
}
.room-img{
  width: 50%;
  margin-top: 40px;
}


</style>
