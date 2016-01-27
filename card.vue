<style scoped>

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
