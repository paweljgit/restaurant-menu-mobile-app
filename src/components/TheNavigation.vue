<template>
<div class="wrapper">
  <div class="scroll-wrapper">
    <nav class="navigation">
      <NavigationItem 
        v-for="(dish, index) in listOfDishes" 
        :key="dish.name+index" 
        :dish="dish"
        :index="index"
        :currentDishIndex="currentDishIndex"
        @click="[
          setCurrent(index), 
          setPositionOfCurrent($event)
        ]"
      />
      <div 
        class="navigation__current-item-indicator" 
        :style="getPositionOfCurrent"
      ></div>
    </nav>
  </div>
</div>
</template>

<script>
import NavigationItem from './NavigationItem'

export default {
  name: 'TheNavigation',
  components: {
    NavigationItem
  },
  data() {
    return {
      positionOfCurrent: 0
    }
  },
  props: {
    listOfDishes: {
      type: Array,
      required: true
    },
    currentDishIndex: {
      type: Number,
      required: true
    }
  },
  computed: {
    getPositionOfCurrent() {
      const itemWidth = 70;
      const itemMargin = 15;
      const numberOfItems = this.currentDishIndex;
      const calculatedValue = (itemWidth+itemMargin)*numberOfItems;
      return `left: ${calculatedValue}px`
    }
  },
  methods: {
    setCurrent (index) {
      this.$emit('change-current-index',index);
    },
    setPositionOfCurrent (element) {
      this.positionOfCurrent = element.target.offsetLeft;
    },
    getDishPictureStyle (index) {
      const thisDish = this.listOfDishes[index]
      return `background-image: url("${thisDish.pic}");`
    }
  } 
}
</script>

<style lang="scss" scoped>

.wrapper {
  position: absolute;
  bottom: 20px;
  width: 100%;
  padding: 0px var(--mobile-x-padding);
  opacity: 0;
  animation: fromBotton 0.5s ease-out;
  animation-delay: 0.5s;
  animation-fill-mode: forwards;
  z-index: -1 !important;
}

.scroll-wrapper {
  width: 100%;
  overflow: scroll;
  height: 130px;

  &::-webkit-scrollbar {
    -webkit-appearance: none;
    width: 0px;
    height: 5px;
    border-bottom: 1px solid rgb(187, 187, 187);
  }

  &::-webkit-scrollbar-thumb {
    border-radius: 0px;
    background-color: rgba(0, 0, 0, 0.151);
    -webkit-box-shadow: 0 0 1px rgba(255, 255, 255, .5);
  }
}

.navigation {
  width: fit-content;
  display: flex;
  flex-direction: row;
  position: relative;

  &__current-item-indicator {
    // same size as navigation item
    height: 115px; 
    width: 70px;
    background-color: rgba(255, 255, 255, 0.26);
    position: absolute;
    transition: all 0.5s ease-in-out;
    border-radius: 7px;
    z-index: -1;
  }
}

@keyframes fromBotton {
  from {
    bottom: -130px;
    opacity: 0;
  }
  to {
    bottom: 20px;
    opacity: 1;
  }
}
</style>