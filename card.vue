<style scoped>
.card{border:1px solid #ccc}
.card-2{box-shadow:0 2px 4px 0 rgba(0,0,0,0.16),0 2px 10px 0 rgba(0,0,0,0.12) !important}
.card-4{box-shadow:0 4px 8px 0 rgba(0,0,0,0.2),0 6px 20px 0 rgba(0,0,0,0.19) !important}
.card-8{box-shadow:0 8px 16px 0 rgba(0,0,0,0.2),0 6px 20px 0 rgba(0,0,0,0.19) !important}
.card-12{box-shadow:0 12px 16px 0 rgba(0,0,0,0.24),0 17px 50px 0 rgba(0,0,0,0.19) !important}
.card-16{box-shadow:0 16px 24px 0 rgba(0,0,0,0.22),0 25px 55px 0 rgba(0,0,0,0.21) !important}
.card-24{box-shadow:0 24px 24px 0 rgba(0,0,0,0.2),0 40px 77px 0 rgba(0,0,0,0.22) !important}
</style>

<template>
<div :class="[cardClass]" :style="{ width: width }">
  <slot></slot>
</div>
</template>

<script lang="babel">
export default {
  props: {
    depth: String,
    width: {
      type: String,
      default(){
        return "100%";
      }
    }
  },
  data(){
    let cardClass = 'card'+((this.depth)?`-${this.depth}`:'');

    return {
      cardClass: cardClass
    }
  }
}
</script>
