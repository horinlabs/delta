<style scoped>
.progress-bar{
  height: 20px;
  position: relative;
}
.progress-bar > .progress{
  float: right;
  height: 100%;
  background-color: #DDD;
}
.progress-bar > .counter{
  position: absolute;
  left: 0px;
  right: 0px;
  top: 0px;
  bottom: 0px;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>

<template>
<div class="progress-bar">
  <div class="progress" :style="{'width': opposite }"></div>
  <div class="counter">{{ percent }}%</div>
</div>
</template>

<script lang="babel">
export default {
  props: {
    actual: Number,
    initial: {
      type: Number,
      default(){
        return 0;
      }
    },
    final: {
      type: Number,
      default(){
        return 100;
      }
    },
  },
  computed: {
    percent(){
      let ratio = (this.actual / (this.final - this.initial)) * 100;
      return ratio;
    },
    opposite(){
      let opposite = 100 - this.percent;
      return `${opposite}%`;
    }
  }
}
</script>
