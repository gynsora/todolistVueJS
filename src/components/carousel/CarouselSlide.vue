<template>
  <transition :name="transitionDirection">
    <div v-show="visible">
      <slot></slot>
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    index: {type: Number, default: 0}
  },
  computed: {
    transitionDirection () {
      if (this.$parent.direction) {
        return 'slide-' + this.$parent.direction
      }
    },
    visible () {
      return this.index === this.$parent.index
    }
  }
}
</script>

<style>
  .slide-right-enter-active {
    animation: slideRightIn .5s ;
  }
  .slide-right-leave-active {
    animation: slideRightOut .5s ;
    position:absolute;
    top:0;
    left:0;
    right:0;
    bottom:0;
  }
  @keyframes slideRightIn {
    from {
      transform: translateX(100%)
    }
    to   { transform: translateX(0)  }
  }
   @keyframes slideRightOut {
    from {
      transform: translateX(0)
    }
    to   { transform: translateX(-100%)  }
  }
  .slide-left-enter-active {
    animation: slideLefttIn .5s ;
  }
  .slide-left-leave-active {
    animation: slideLeftOut .5s ;
    position:absolute;
    top:0;
    left:0;
    right:0;
    bottom:0;
  }

  @keyframes slideLefttIn {
    from {
      transform: translateX(-100%)
    }
    to   { transform: translateX(0)  }
  }
   @keyframes slideLeftOut {
    from {
      transform: translateX(0)
    }
    to   { transform: translateX(100%)  }
  }

</style>
