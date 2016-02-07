<style scoped>
.dropdown-click,.dropdown-hover{
  cursor:pointer;
  position:relative;
  display:inline-block;
}
.dropdown-click button,.dropdown-hover button{
  background-color: transparent;
  border: 0px none;
  padding: 5px 9px;
}
.dropdown-hover:hover .dropdown-content{
  z-index:1;
  display:block;
}
.dropdown-content{
  margin:0;
  padding:0;
  display:none;
  color:#656565;
  min-width:160px;
  position:absolute;
  background-color:#FFF;
}
.dropdown-content a{
  display:block;
  padding:6px 16px;
}
.dropdown-content a:hover{
  background-color:#CCC;
}
</style>

<template>
<div :class="[(clickable)?'dropdown-click':'dropdown-hover']">
  <button type="button" @click="toggleDropdown"><slot></slot><span class="caret"></span></button>
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
