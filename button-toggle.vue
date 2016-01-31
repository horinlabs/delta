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
.btn-toggle.on::after{
  content: 'Yes';
}
.btn-toggle.off::before{
  content: 'No';
}
.btn-toggle.on::after,
.btn-toggle.off::before{
  position: absolute;
  left: 0px;
  right: 0px;
  top: 0px;
  bottom: 0px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.btn-toggle.on > .key{
  left: 1px;
}
.btn-toggle.off > .key{
  right: 1px;
}
</style>

<template>
<div class="btn-toggle" :class="{'on': value, 'off': !value}" @click="value = !value">
  <input type="checkbox" :name="name" v-model="value">
  <div class="key"></div>
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
