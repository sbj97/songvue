<template>
    <div class="discount">
    <h4>지금사면 {{amount}}%할인</h4>
  </div>

</template>

<script>
export default {
     name: 'DiscountBanner',
     props : {
      amount : Object,
     }
}
</script>

<style>

</style>