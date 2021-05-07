<template>
<div class="desc">
  <transition name="fade">
    <span 
      class="desc__text"
      :key="Math.random()"
    >  
      {{ getCurrentDishDescription }}
    </span>
  </transition>
</div>
</template>

<script>

export default {
  name: 'TheDishDescription',
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
    getCurrentDishDescription() {
      return this.listOfDishes[this.currentDishIndex].description
    }
  }
}
</script>

<style lang="scss" scoped>

.desc {
  width: 100%;
  position: relative;
  border-top: 1px solid rgba(0, 0, 0, 0.082);

  &__text {
    color: rgba(0, 0, 0, 0.575);
    display: block;
    position: absolute;
    top: 0px;
    width: 100%;
    height: 60px;
    padding-top: 5px;
    overflow: scroll;
    font-size: 12px;
  }

  &__text::-webkit-scrollbar {
    display: none;
  }
}

// Fade animation

.fade-enter-active {
  animation: fade-in 0.5s ease-in;
  animation-delay: 0.5s;
  opacity: 0;
}

.fade-leave-active {
  animation: fade-out 0.5s ease-out;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}

@keyframes fade-out {
  from { opacity: 1 }
  to { opacity: 0 }
}

@keyframes fade-in {
  from { opacity: 0 }
  to { opacity: 1 }
}

</style>