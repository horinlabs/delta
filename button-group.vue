<style>
.btn-group{
  display: inline-block;
}
.btn-group .btn{
  float:left;
}
</style>

<template>
<div class="btn-group">
  <slot></slot>
</div>
</template>

<script lang="babel">
export default {
  props: ["size"],
  ready(){
    Array.prototype.forEach.call(this.$el.children, (button) => button.classList.add(this.size));
  }
}
</script>
