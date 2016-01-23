<style scoped>

</style>

<template>
<div class="accordion">
  <slot></slot>
</div>
</template>

<script lang="babel">
import AccordionItem from 'accordion-item.vue'

export default {
  props: {
    oneAtTime: Boolean
  },
  components: {
    'accordion-item': AccordionItem
  }
}
</script>
