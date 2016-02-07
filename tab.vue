<style scoped>

</style>

<template>
  <div class="tab-pane" :class="{'active': active}">
    <slot></slot>
  </div>
</template>

<script lang="babel">
export default {
  props: {
    title: String,
    active: Boolean,
    disabled: Boolean,
  },
  events:{
    'tab-selected'(tab){
      this.active = (this.$el === tab);
    }
  }
}
</script>
