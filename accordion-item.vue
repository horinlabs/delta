<style scoped>
.accordion-item{
  margin-bottom: 5px;
}
.accordion-item-body{
  width: 100;
  background-color: white;
  color: #333;
}
</style>

<template>
<div class="accordion-item">
  <header class="container" @click="itemChoosed()">
    <h4>{{title}}</h4>
  </header>
  <div class="container accordion-item-body" v-show="!hidden">
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
