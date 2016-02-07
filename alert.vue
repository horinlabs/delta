<style scoped>

</style>

<template>
<div class="alert container sand" v-show="!hidden">
  <i class="fa" :class="['fa-'+icon]"></i>{{ message }}
  <span class="closebtn" @click="hidden = true">&times;</span>
</div>
</template>

<script lang="babel">
export default {
  props: {
    hidden: Boolean,
    icon: String,
    message: String,
    time: {
      type: Number,
      default(){
        return 0;
      }
    }
  },
  ready(){
    if(this.time > 0){
      setTimeout(() => this.hidden = true, this.time);
    }
  },
  watch: {
    hidden(value){
      value && this.$dispatch('alert-hidden');
    }
  }
}
</script>
