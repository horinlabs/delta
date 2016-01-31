<style scoped>
.select-box{
  height: 30px;
  position: relative;
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
.select-list-item:hover{
  background-color: rgba(129, 200, 208, 0.25);
}
.select-list-item.active{
  background-color: rgba(129, 200, 208, 0.35);
}
</style>

<template>
<div class="select-box">
  <select style="display: none" v-model="selected" :multiple="multiple">
    <option v-for="option in options" :value="option.value">{{ option.text }}</option>
  </select>
  <div class="select" :class="{'open': hidden, 'closed': !hidden}" @click="toggle()">
    {{ getOptionByValue(selected).text }}
  </div>
  <div class="select-list" v-show="!hidden">
    <input type="text" v-el:search v-model="filterKey" class="input">
    <ul class="ul border">
      <li
        class="select-list-item"
        v-for="option in options | filterBy filterKey"
        :class="{'active': getOptionByValue(selected) === option }"
        @click="setSelected(option.value)">
          {{ option.text }}
      </li>
    </ul>
  </div>
</div>
</template>

<script lang="babel">
export default {
  props: {
    options: Array,
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
    multiple: {
      type: Boolean,
      default(){
        return false;
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
    toggle(){
      if(this.hidden){
        this.open();
      } else {
        this.close();
      }
    },
    getOptionByValue(value){
      let filtered = this.options.filter((option) => option.value === value);
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
