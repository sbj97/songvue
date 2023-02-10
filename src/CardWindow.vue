<template>
  <!--main-->
<div>
    <img :src="data.image" class="room-img">
    <h4 @click="send">{{data.title}}</h4>
    <h3>{{data.price}} 원</h3>
    <button @click="increase()">허위매물신고</button>
    <p>신고수 : {{count}}</p>
</div>
</template>

<script>
export default {
    name : 'CardWindow',
    data(){
        return{
            count : 0,
        }
    },
    props : {
        data : Object,
    },
    methods: {
        send(){
            this.$emit('openModal',this.data.id)            
        },
        increase(){
            this.count++;
        },
    },
}
</script>

<style>

</style>