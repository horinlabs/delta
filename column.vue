<style scoped>

</style>

<template>
<div class="col" :class="[size]">
  <slot></slot>
</div>
</template>

<script lang="babel">
export default {
  props: {
    size: String
  }
}
</script>
