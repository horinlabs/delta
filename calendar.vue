<style scoped>
a {
	text-decoration: none;
}

h2 {
	font-size: 2em;
	line-height: 1.25em;
	margin: .25em 0;
}

h3 {
	font-size: 1.5em;
	line-height: 1em;
	margin: .33em 0;
}

.calendar {
	text-align: center;
}

.calendar header {
	position: relative;
}

.calendar h2 {
	text-transform: uppercase;
}

li{
  float:left;
  list-style:none;
  width:calc(100%/7);
}

li.begin{
  clear:both;
}

li > a{
  text-decoration:none;
}

.calendar ul.head {
	font-weight: 600;
	text-transform: uppercase;
}

.calendar ul.body {
	color: #7c8a95;
}

.calendar ul.body li:hover {
	background: #00addf;
}

.calendar ul.body li {
	border-radius: 5%;
	display: inline-block;
	line-height: 4em;
	text-align: center;
}

.calendar .prev-month,
.calendar .next-month {
	color: #cbd1d2;
}

.calendar .prev-month:hover,
.calendar .next-month:hover {
	background-color: #cbd1d2;
}

.current-day {
	background: #00addf;
	color: #f9f9f9;
}

.event {
	cursor: pointer;
	position: relative;
}

.event:after {
	background: #00addf;
	border-radius: 5%;
	bottom: .5em;
	display: block;
	content: '';
	height: .5em;
	left: 50%;
	margin: -.25em 0 0 -.25em;
	position: absolute;
	width: .5em;
}

.event.current-day:after {
	background: #f9f9f9;
}

.btn-prev,
.btn-next {
	border: 2px solid #cbd1d2;
	border-radius: 50%;
	color: #cbd1d2;
	height: 2em;
	font-size: .75em;
	line-height: 2em;
	margin: -1em;
	position: absolute;
	top: 50%;
	width: 2em;
}

.btn-prev:hover,
.btn-next:hover {
	background: #cbd1d2;
	color: #f9f9f9;
}

.btn-prev {
	left: 6em;
}

.btn-next {
	right: 6em;
}
</style>

<template>
  <div class="calendar">
		<header>
			<h2>{{ monthName }} - {{ year }}</h2>
			<a class="btn-prev" @click="previousMonth()"><i class="fa fa-angle-left"></i></a>
			<a class="btn-next" @click="nextMonth()"><i class="fa fa-angle-right"></i></a>
		</header>
  	<ul class="head">
      <li :class="{'begin': $index == 0}" v-for="week in weekNames">{{ week }}</li>
  	</ul>
  	<ul class="body">
      <li
			@click="setDate(day)"
      v-for="day in days"
      v-bind:class="{
        'begin': $index % 7 == 0,
        'current-day': day.getMonth() == currentDate.getMonth() && day.getDate() == currentDate.getDate() && day.getFullYear() == currentDate.getFullYear(),
        'prev-month': day.getMonth() < month,
        'next-month': day.getMonth() > month
    	}">
        {{ day.getDate() }}
      </li>
    </ul>
	</div>
</template>

<script lang="babel">
let
getCalendar = function(month, _year, locale){
	let
	days = [],
	date = new Date(_year, month, 1),
	dayOfWeek = date.getDay(),
	monthName = date.toLocaleString(locale, { month: "long" }),
	capitalize = function(str){
		return str.replace(/(?:^|\s)\S/g, function(a){ return a.toUpperCase() });
	};

	date.setDate(1-dayOfWeek);
	let previousMonth = (month === 0)? 11 : month - 1;

	while (date.getMonth() === previousMonth) {
		days.push(new Date(date));
		date.setDate(date.getDate() + 1);
	}

	while (date.getMonth() === month) {
		days.push(new Date(date));
		date.setDate(date.getDate() + 1);
	}

	dayOfWeek = date.getDay();
	let finalDate = new Date(date).setDate(date.getDate() + 6 - dayOfWeek);

	while (date <= finalDate) {
		days.push(new Date(date));
		date.setDate(date.getDate() + 1);
	}

	return {
		days: days,
		month: month,
		year: _year,
		monthName: capitalize(monthName)
	};
}

export default {
  props: {
    currentDate: {
			type: Date,
			default(){
				return new Date();
			}
		},
		locale: {
			type: String,
			default(){
    		return "en";
			}
		},
    weekNames: {
			type: Array,
			default(){
    		return ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];
			}
		}
  },
  data(){
    return getCalendar(this.currentDate.getMonth(), this.currentDate.getFullYear(), this.locale);
  },
	methods:{
	  nextMonth(){
			if(this.month == 11){ this.month = 0; this.year++; }
			else this.month++;

			Object.assign(this, getCalendar(this.month, this.year, this.locale));
	  },
	  previousMonth(){
			if(this.month == 0){ this.month = 11; this.year--; }
			else this.month--;

	    Object.assign(this, getCalendar(this.month, this.year, this.locale));
	  },
		setDate(date){
			this.$nextTick(() => {
				this.currentDate = date;
				this.month = date.getMonth();
				Object.assign(this, getCalendar(this.month, this.year, this.locale));
				this.$emit('date-changed');
			})
		}
	}
}
</script>
