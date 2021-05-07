<template>
<div class="carousel">
  <CarouselItem 
    v-for="(dish, index) in listOfDishes" 
    :key="dish.name+index" 
    :currentDishIndex="currentDishIndex" 
    :previousDishIndex="previousDishIndex"
    :itemIndex="index"
    :dish="listOfDishes[index]"
    @item-swiped="emitSwiped"
  />
</div>
</template>

<script>
import CarouselItem from './CarouselItem';

export default {
  name: 'TheCarousel',
  components : {
    CarouselItem
  },
  props: {
    listOfDishes: {
      type: Array,
      require: true,
    },
    currentDishIndex: {
      type: Number,
      require: true,
      default: 0
    },
    previousDishIndex: {
      type: Number,
      require: true,
      default: 0
    }
  },
  methods: {
    emitSwiped(e) {
      this.$emit('item-swiped',e)
    }
  }
}
</script>

<style lang="scss" scoped> 

.carousel {
  position: relative;
  width: 320px;
  height: 320px;
  opacity:0;
  animation: fromTop 0.5s ease-out;
  animation-delay: 0.2s;
  animation-fill-mode: forwards;

  &::before {
    display: block;
    content: "";
    position: absolute;
    top: -178%;
    left: -50%;
    width: 200%;
    height: 200%;
    border-radius: 50%;
    box-sizing: border-box;
    border: 80px solid rgba(255, 166, 0, 0.15);
    margin-top: 60px;
  }

}

@keyframes fromTop {
    from {
        top: -50%;
        opacity:0;
    }
    to {
      top: 0px;
      opacity:1;
    }
}
</style>
