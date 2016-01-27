<style scoped>
.overlay{
  z-index: 50px;
  background: rgba(255, 255, 255, 0.7);
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}
.overlay > i{
  position: absolute;
  top: 50%;
  left: 50%;
  margin-left: -15px;
  margin-top: -15px;
  font-size: 30px;
}
</style>

<template>
<div class="overlay">
  <i class="fa fa-spinner fa-pulse"></i>
  <!-- <p>{{ loadingMessage }}</p> -->
</div>
</template>

<script lang="babel">
export default {
  props: {
    loadingMessage: {
      type: String,
      default(){
        return "Loading";
      }
    }
  }
}
</script>
