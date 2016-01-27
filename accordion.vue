<style scoped>

</style>

<template>
<div class="accordion" @item-choosed="resolveItem()">
  <slot></slot>
</div>
</template>

<script lang="babel">
export default {
  props: {
    oneAtTime: Boolean
  },
  methods: {
    resolveItem(a,b,c,d,e){
      console.log("Frango",a,b,c,d,e);
    }
  }
}
</script>
