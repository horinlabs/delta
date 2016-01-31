<style scoped>

</style>

<template>
<ul class="pagination border round">
  <li v-if="arrows" @click="previousPage"><a href="#">&laquo;</a></li>
  <li v-for="page in pages">
    <a href="#" :class="[(active == page + 1)?activeClass:'']" @click="changePage(page + 1)">{{ page + 1 }}</a>
  </li>
  <li v-if="arrows" @click="nextPage"><a href="#">&raquo;</a></li>
</ul>
</template>

<script lang="babel">
export default {
  props: {
    arrows: Boolean,
    pages: {
      type: Number,
      default(){
        return 1;
      }
    },
    activeClass: {
      type: String,
      default(){
        return "blue";
      }
    },
    active: {
      type: Number,
      default(){
        return 1;
      }
    }
  },
  methods: {
    changePage(page){
      this.active = page;
      this.$emit('page-changed', this.active);
    },
    previousPage(){
      if(this.active > 0) this.changePage(this.active - 1);
    },
    nextPage(){
      if(this.active <= this.pages) this.changePage(this.active + 1);
    },
  }
}
</script>
