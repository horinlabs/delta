<style scoped>

</style>

<template>
<div :class="[(clickable)?'dropdown-click':'dropdown-hover']">
  <button type="button" @click="toggleDropdown"><slot></slot></button>
  <div class="dropdown-content" :class="[(open)?'show':'']">
    <a :href="link.page" v-for="link in links">{{ link.text }}</a>
  </div>
</div>
</template>

<script lang="babel">
export default {
  props: {
    clickable: Boolean,
    links: {
      type: Array,
      default(){
        return [];
      }
    }
  },
  data(){
    return { open: false };
  },
  methods: {
    toggleDropdown(){
      if(this.clickable){
        this.open = !this.open;
        this.$emit('dropdown-clicked', this.open);
      }
    }
  }
}
</script>
