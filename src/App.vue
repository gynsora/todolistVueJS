<template>
  <div id="app">
    <carousel>
      <carousel-slide v-for="n in slides" :index="n-1">
        <div style="position: absolute; left:0 ; right:0 ;text-align:center; top:50% ;color: #fff; font-size:17px;background-color:grey;">
          Salut les gens {{ n }}
        </div>
        <img :src="'https://picsum.photos/id/'+ n +'/600/300'" width="100%" >
      </carousel-slide>
    </carousel>
    <button @click="addSlide">Ajouter un slide</button>
    <button @click="removeSlide">Supprimer un slide</button>
    <Todos></Todos>
  </div>
</template>

<script>
import Todos from './components/Todos'
import Carousel from './components/carousel/Carousel'
import CarouselSlide from './components/carousel/CarouselSlide'
export default {
  name: 'App',
  data () {
    return {
      slides: 5
    }
  },
  components: {
    Todos,
    Carousel,
    CarouselSlide
  },
  methods: {
    addSlide () {
      this.slides++
    },
    removeSlide () {
      this.slides--
    }
  }
}
</script>

<style>

</style>
