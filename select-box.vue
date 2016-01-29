<style scoped>
.select{
  height: 30px;
  margin-bottom: 5px;
}
.open::after {
  display: inline-block;
  width: 0;
  height: 0;
  border-top: 5px solid #000;
  border-right: 5px solid transparent;
  border-left: 5px solid transparent;

  position: absolute;
  right: 2px;
  content:'';
}
.closed::after {
  display: inline-block;
  width: 0;
  height: 0;
  border-bottom: 5px solid #000;
  border-right: 5px solid transparent;
  border-left: 5px solid transparent;

  position: absolute;
  right: 2px;
  content:'';
}
.select-list{
  width: 100;
  background-color: white;
  color: #333;
}
</style>

<template>
<div class="">
  <select style="display: none" v-model="selected">
    <option v-for="option in options" :value="option.value">{{ option.text }}</option>
  </select>
  <div class="select" :class="{'open': hidden, 'closed': !hidden}" @click="openSelect()">
    {{ selected }}
  </div>
  <div class="select-list" v-show="!hidden">
    <input type="text" v-model="filterKey" class="input" @blur="openSelect()">
    <ul class="ul border">
      <li v-for="option in options | filterBy filterKey" @click="setSelected(option.value)">{{ option.text }}</li>
    </ul>
  </div>
</div>
</template>

<script lang="babel">
export default {
  props: {
    filterKey: {
      type: String,
      default(){
        return '';
      }
    },
    options: Array,
    hidden: {
      type: Boolean,
      default(){
        return true;
      }
    },
    selected: {
      type: String,
      default(){
        return '';
      }
    }
  },
  methods: {
    openSelect(){
      this.hidden = !this.hidden;
      this.$emit('select-open', this.$el);
    },
    setSelected(value){
      this.hidden = true;
      this.filterKey = '';
      this.selected = value;
      this.$emit('item-selected', {value: value, el: this.$el});
    }
  }
}
</script>
