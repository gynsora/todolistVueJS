<template>
  <div class="carousel">
    <slot></slot>
    <button class="carousel__nav carousel__prev" @click.prevent="prev"></button>
    <button class="carousel__nav carousel__next" @click.prevent="next"></button>
    <div class="carousel_pagination">
      <button v-for="n in slideCount" @click="goto(n-1)" :class="{active: n - 1 === index}"></button>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      index: 0,
      slides: [],
      direction: 'right'
    }
  },
  watch: {
    slides (slides) {
      if (this.index >= this.slideCount) {
        this.index = this.slideCount - 1
      }
    }
  },
  mounted () {
    this.slides = this.$children
  },
  methods: {
    next () {
      this.index++
      this.direction = 'right'
      if (this.index >= this.slideCount) {
        this.index = 0
      }
    },
    prev () {
      this.index--
      this.direction = 'left'
      if (this.index < 0) {
        this.index = this.slideCount - 1
      }
    },
    goto (index) {
      this.direction = index > this.index ? 'right' : 'left'
      this.index = index
    }
  },
  computed: {
    slideCount () {
      return this.slides.length
    }
  }
}
</script>

<style>
  .carousel{
    position:relative;
    overflow:hidden;
  }
  .carousel__nav{
    position:absolute;
    top:50%;
    margin-top:-31px;
    left:10px;
    width:60px;
    height:60px;
    background: url(../../assets/prev.jpg);
    background-size:  cover;

  }
  .carousel__nav.carousel__next{
    right: 1px ;
    left:auto ;
    background: url(../../assets/next.jpg);
    background-size:  cover;
    cursor:pointer;
  }
  .carousel__nav.carousel__prev{
    cursor:pointer;
  }
  .carousel_pagination{
    position:absolute;
    bottom:10px;
    right:0;
    left:0;
    text-align: center;
  }
  .carousel_pagination button{
    cursor:pointer;
    display:inline-block;
    height:10px;
    width:10px;
    background-color: #000;
    opacity:.8;
    border-radius:10px;
  }
  .carousel_pagination .active{
    background-color: #fff;
  }
</style>
