<style scoped>
.select-box{
  height: 30px;
  position: relative;
  margin-bottom: 5px;
}
.select-box > .select{
  padding:4px 0;
  width:100%;
  color:#000;
  border:1px solid transparent;
  border-bottom:1px solid #009688;
}
.select-box > .select.open::after {
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
.select-box > .select.closed::after {
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
.select-box > .select-list{
  width: 100;
  background-color: white;
  color: #333;
}
.select-box > .select-list .select-list-item:hover{
  background-color: rgba(129, 200, 208, 0.25);
}
.select-box > .select-list .select-list-item.active{
  background-color: rgba(129, 200, 208, 0.35);
}
</style>

<template>
<div class="select-box">
  <select style="display: none" v-model="selected" :multiple="multiple">
    <option v-for="option in options" :value="option[valueKey]">{{ option[textKey] }}</option>
  </select>
  <div class="select" :class="{'open': hidden, 'closed': !hidden}" @click="toggle()">
    {{ getOptionByValue(selected)[textKey] }}
  </div>
  <div class="select-list" v-show="!hidden">
    <input type="text" v-el:search v-model="filterKey" class="input">
    <ul class="ul border">
      <li
        class="select-list-item"
        v-for="option in options | filterBy filterKey"
        :class="{'active': getOptionByValue(selected) === option }"
        @click="setSelected(option[valueKey])">
          {{ option[textKey] }}
      </li>
    </ul>
  </div>
</div>
</template>

<script lang="babel">
export default {
  props: {
    options: Array,
    multiple: Boolean,
    filterKey: {
      type: String,
      default(){
        return '';
      }
    },
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
    },
    textKey: {
      type: String,
      default(){
        return 'text';
      }
    },
    valueKey: {
      type: String,
      default(){
        return 'value';
      }
    }
  },
  methods: {
    toggle(){
      if(this.hidden){
        this.open();
      } else {
        this.close();
      }
    },
    getOptionByValue(value){
      let filtered = this.options.filter((option) => option[this.valueKey] === value);
      return filtered[0] || {};
    },
    open(){
      this.hidden = false;
      this.$nextTick(() => this.$els.search.focus());
      this.$emit('select-opened', this.$el);
    },
    close(){
      this.hidden = true;
      this.filterKey = '';
      this.$emit('select-closed', this.$el);
    },
    setSelected(value){
      this.selected = value;
      this.close();
      this.$emit('item-selected', {value: value, el: this.$el});
    }
  }
}
</script>
