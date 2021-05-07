<template>
<transition :name="getSlideDirection()" >
  <div v-if="visible" class="dish-wrapper" >
    <div class="dish" @touchstart="touchStart">
      <div 
        :style="getDishPictureStyle" 
        class="dish__picture"
      ></div>
    </div>
  </div>
</transition>
</template>

<script>
export default {
  name: 'CarouselItem',
  props: {
    dish: {
      type: Object,
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
    },
    itemIndex: {
      type: Number,
      require: true
    }
  },
  computed: {
    visible() {
      return this.itemIndex === this.currentDishIndex;
    },
    getDishPictureStyle () {
      return `background-image: url("${this.dish.pic}");`
    },
  },
  methods: {
    getSlideDirection () {
      if (this.currentDishIndex > this.previousDishIndex) {
        return 'slide-right'
      } else {
        return 'slide-left'
      }
    },
    touchStart (touchEvent) {
      if (touchEvent.changedTouches.length !== 1) { // We only care if one finger is used
        return;
      }
      const posXStart = touchEvent.changedTouches[0].clientX;
      addEventListener('touchend', (touchEvent) => this.touchEnd(touchEvent, posXStart), {once: true});
    },
    touchEnd (touchEvent, posXStart) {
      if (touchEvent.changedTouches.length !== 1) { // We only care if one finger is used
        return;
      }
      const posXEnd = touchEvent.changedTouches[0].clientX;
      if (posXStart < posXEnd) {
        this.$emit('item-swiped', 'left')
      } else if (posXStart > posXEnd) {
        this.$emit('item-swiped', 'right')
      }
    }
  }
}
</script>

<style lang="scss" scoped> 

.dish-wrapper {
  position:absolute;
  top:-160%;
  left:-50%;
  width: 200%;
  height: 200%;
  transform: rotate(45deg);
}

.dish {
  width: 30%;
  height: 30%;
  position: absolute;
  bottom:0;
  right:0;
  border-radius: 50%;
  transform: rotate(-45deg);
  box-shadow: rgba(0, 0, 0, 0.637) 0px 4px 12px;

  &__picture {
    width: 100%;
    height: 100%;
    background-size: cover;
    background-position: 50% 50%;
  }
}

// slide-right animation

.slide-right-enter-active {
  animation: slide-right-in 0.5s ease-in;
}

.slide-right-leave-active {
  animation: slide-right-out 0.5s ease-in;
}

@keyframes slide-right-out {
  from { transform: rotate(45deg) }
  to { transform: rotate(135deg) }
}

@keyframes slide-right-in {
  from { transform: rotate(-45deg) }
  to { transform: rotate(45deg) }
}


// slide-left animation

.slide-left-enter-active {
  animation: slide-left-in 0.5s ease-in;
}

.slide-left-leave-active {
  animation: slide-left-out 0.5s ease-in;
}

@keyframes slide-left-out {
  from { transform: rotate(45deg) }
  to { transform: rotate(-45deg) }
}

@keyframes slide-left-in {
  from { transform: rotate(135deg) }
  to { transform: rotate(45deg) }
}

</style>
