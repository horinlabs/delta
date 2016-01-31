<style scoped>
.breadcrumb > span:not(.active){
  color: lightgrey;
}
.breadcrumb > span + span::before{
  content: ">";
  color: grey;
}
</style>

<template>
<div class="breadcrumb">
  <span v-for="item in items" :class="{'active': $index === (items.length - 1) }">
    {{ item }}
  </span>
</div>
</template>

<script lang="babel">
export default {
  props: {
    items: Array
  }
}
</script>
