<style scoped>
.datepicker{
  height: 30px;
}
.datepicker > .calendar {
  position: absolute;
  width: 400px;
}
</style>

<template>
<div class="datepicker" :style="{ 'width': width }">
  <input type="text" class="input" @focus="showCalendar = true" @blur="showCalendar = false" v-model="dateString">
  <calendar v-show="showCalendar" :current-date.sync="selectedDate"></calendar>
</div>
</template>

<script lang="babel">
import Calendar from './calendar'

export default {
  props: {
    width: String,
    // time: {
    //   type: Boolean,
    //   default(){
    //     return false;
    //   }
    // },
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
