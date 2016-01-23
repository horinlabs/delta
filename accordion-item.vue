<style scoped>

</style>

<template>
<div class="accordion-item">
  <div class="accordion-item-header">
    {{title}}
  </div>
  <div class="accordion-item-body" v-if="{{ !hidden }}">
    <slot></slot>
  </div>
</div>
</template>

<script lang="babel">
export default {
  props: {
    title: String,
    hidden: Boolean
  }
}
</script>
