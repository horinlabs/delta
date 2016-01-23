<style scoped>
input {
  width: 100%;
}
</style>

<template>
<div class="container" :style="{ 'width': width }">
  <input type="text" @focus="showCalendar = true" @blur="showCalendar = false" v-model="dateString">
  <calendar v-show="showCalendar" :current-date.sync="selectedDate"></calendar>
</div>
</template>

<script lang="babel">
import Calendar from './calendar'

export default {
  props: {
    width: String,
    showCalendar: {
      type: Boolean,
      default(){
        return false;
      }
    },
    selectedDate: {
      type: Date,
      default(){
        return new Date();
      }
    }
  },
  computed:{
    dateString(){
      return this.selectedDate.toLocaleDateString();
      //TODO ou "dd/MMM/YYYY".replace("dd", 23).replace("mm", 01).replace("MMM", "Jan").replace("YYYY", 2016);
    }
  },
  components: {
    Calendar
  }
}
</script>
