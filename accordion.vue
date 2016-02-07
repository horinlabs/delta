<style scoped>

</style>

<template>
<div class="accordion">
  <slot></slot>
</div>
</template>

<script lang="babel">
export default {
  props: {
    oneAtTime: Boolean
  },
  events: {
    'accordion-item-choosed'(item){
      if(this.oneAtTime){
        this.$children.forEach((child) => child.hidden = (child.$el != item));
      }
    }
  }
}
</script>
