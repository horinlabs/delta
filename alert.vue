<style scoped>

</style>

<template>
<div class="alert" v-show="!hidden">
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
        return 10000;
      }
    }
  }
}
</script>
