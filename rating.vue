<style scoped>

</style>

<template>
<div class="rating">
  <input type="hidden" v-model="rate">
  <span v-for="n in max" @click="rate = n + 1" class="fa" :class="{'fa-star-o': n >= rate, 'fa-star': n < rate}"></span>
</div>
</template>

<script lang="babel">
  export default {
    props: {
      rate: {
        type: Number,
        default(){
          return 0;
        }
      },
      max: {
        type: Number,
        default(){
          return 5;
        }
      }
    }
  }
</script>
