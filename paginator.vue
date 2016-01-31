<style scoped>
.pagination{
  margin:0;
  padding:0;
  display:inline-block;
}
.pagination li{
  display:inline;
}
.pagination li a{
  color:#000;
  float:left;
  padding:8px 16px;
  text-decoration:none;
  transition:background-color .3s;
}
.pagination li a:hover,.pagination li a:focus{
  background-color:#ccc;
}
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
