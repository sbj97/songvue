<template>
  <!--modal-->
  <div class="black-bg" v-if="modal == true">
    <div class="white-bg">
      <img :src="data[clickCheck].image" style="width:50%">
      <h4>{{data[clickCheck].title}}</h4>
        <p>{{data[clickCheck].content}}</p>
        <input v-model="month">
        <p>{{month}}개월 선택함 : {{data[clickCheck].price * month}}
        원</p>

        <button @click="modalClose">닫기</button>        
    </div>
  </div>
  </template>

<script>
export default {
    name : 'ModalPopup',
    data(){
      return{
        month : 1,
        
      }      
    },
    watch :{
      month(a){
        if(a >= 13){
          alert('13이상 입력하지 말아주세요');
          this.month = 1;
        }
        if(isNaN(a) == true){
          alert('문자입력하지마샘');
          this.month = 1;
        }
      },
    },

    props :{ 
      data : Array,
      clickCheck : Number,
      modal : Boolean,
    },
    methods :{
       modalClose(){
            this.$emit('modalPopupClose')
       } 
    },
}
</script>

<style>

</style>