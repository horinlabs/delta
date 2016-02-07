<style>
.tab-container > .tab-menu{
  /*display: inline;*/
  height: 45px;
}
.tab-container > .tab-menu > p{
  cursor: pointer;
  color: #E9E9E9;
  float: left;
  margin: 0px;
  padding: 10px 30px;
  border-bottom: 2px solid transparent;
}
.tab-container > .tab-menu > p.active{
  color: #FFF;
  border-bottom-color: yellow;
}
.tab-container > .tab{
  color: #000;
  padding: 10px;
  background-color: white;
}
.tab-container > .tab > .tab-pane{
  display:none;
}
.tab-container > .tab > .tab-pane.active{
  display:block;
}
</style>

<template>
<div class="tab-container">
  <nav class="tab-menu">
    <p v-for="child in $children" @click="setActive(child)" :class="{'active': $index == active}">{{ child.title }}</p>
  </nav>
  <div class="tab">
    <slot></slot>
  </div>
</div>
</template>

<script lang="babel">
export default {
  props: {
    active: {
      type: Number,
      default(){
        return 0;
      }
    }
  },
  ready(){
    this.setActive(this.$children[this.active]);
  },
  methods: {
    setActive(tab){
      this.active = this.$children.indexOf(tab);
      this.$broadcast('tab-selected', tab.$el);
    }
  }
}
</script>
