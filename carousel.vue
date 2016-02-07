<style>
.carousel{
  min-height: 250px;
  position: relative;
  overflow: hidden;
}
.carousel.left > .slider{ left: 0px }
.carousel.top > .slider{ top: 0px }

.carousel.left,
.carousel.left > .previous,
.carousel.left > .next{
  float: left;
}

.carousel.left > .slider {
  height: 100%;
}
.carousel.top > .slider {
  width: 100%;
}
.carousel > .slider {
  overflow: hidden;
  margin: 7px auto;
  height: 100%;
  width: 100%;
  position: absolute;
  transition: left 1s ease 0.1s, top 1s ease 0.1s;
}
.carousel > .slider > .item{
  float: left;
  overflow: hidden;
  width: 100%;
}
.carousel.left > .slider > .item{
  left: 100%;
}
.carousel.top > .slider > .item{
  top: 100%;
}
</style>

<template>
<div class="carousel" :class="[side]">
  <!-- <ul>
    <li v-for="slide in items"><a @click="showSlide($index)">x</a></li>
  </ul> -->
  <div class="previous"></div>
  <div class="slider" :style="sliderStyle" v-el:slider>
    <article class="item" v-for="slide in items" :style="itemStyle">
      <img :src="slide.image" :alt="slide.title" />
      <div class="">
        <span>{{ slide.title }}</span>
        <span>{{ slide.text }}</span>
      </div>
    </article>
  </div>
  <div class="next"></div>
</div>
</template>

<script lang="babel">
export default {
  props: {
    items: Array,
    interval: Number,
    direction: {
      type: String,
      default(){
        return 'left';
      }
    },
    current: {
      type: Number,
      default(){
        return 0;
      }
    }
  },
  data(){
    let dimension = this.direction === 'left' ? 'width': 'height';

    return {
      sliding: false,
      currentSlide: 0,
      sliderStyle: {
        [this.direction]: '0%',
        [dimension]: `${this.items.length * 100}%`,
      },
      itemStyle: {
        [dimension]: `${100 / this.items.length}%`
      }
    }
  },
  ready(){
    this.$els.slider.addEventListener('transitionend', () => this.sliding = false);
    setInterval(() => this.next(), this.interval);
  },
  methods: {
    showSlide: function(slideNumber) {
      if(this.sliding) return;
      this.sliding = true;
      this.sliderStyle[this.direction] = `-${slideNumber * 100}%`;
    },
    next: function(){
      if(this.currentSlide == this.items.length - 1) this.currentSlide = -1;
      if(!this.sliding) this.showSlide(++this.currentSlide);
    },
    previous: function(){
      if(this.currentSlide == 0) this.currentSlide = this.items.length;
      if(!this.sliding) this.showSlide(--this.currentSlide);
    },
  }
}
</script>
