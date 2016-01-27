<style scoped>

</style>

<template>
<div class="container">
  <header class="container" @click="itemChoosed()">
    <h4>{{title}}</h4>
  </header>
  <div class="container" v-show="!hidden">
    <slot></slot>
  </div>
</div>
</template>

<script lang="babel">
export default {
  props: {
    title: String,
    hidden: {
      type: Boolean,
      default(){
        return true;
      }
    }
  },
  methods: {
    itemChoosed(){
      this.hidden = !this.hidden;
      this.$emit('item-choosed', this.$el);
    }
  }
}
</script>
