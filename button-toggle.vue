<style scoped>
.btn-toggle{
  height: 35px;
  width: 50px;
  position: relative;
  margin: 2px;
}
.btn-toggle > input[type=checkbox]{
  display: none;
}
.btn-toggle > .key{
  position: absolute;
  top: 1px;
  bottom: 1px;
  width: 6px;
  background-color: white;
}
.btn-toggle > .key.on{
  left: 1px;
}
.btn-toggle > .key.off{
  right: 1px;
}
</style>

<template>
<div class="btn-toggle" @click="value = !value">
  <input type="checkbox" :name="name" v-model="value">
  <div class="key" :class="{'on': value, 'off': !value}"></div>
</div>
</template>

<script lang="babel">
export default {
  props: {
    value: Boolean,
    name: String
  }
}
</script>
