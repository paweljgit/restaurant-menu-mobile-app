<template>
<div 
  class="dish-name" 
  :style="getDishNameStyle"
>
    <transition name="from-left">
      <span 
        class="dish-name__first-part" 
        :style="[
          getDishNamePartStyle,
          resizeFontByNameLenght(getFirstPartOfName)
        ]"
        :key="Math.random()"
      >          
        {{ getFirstPartOfName }}
      </span>
    </transition>
    <transition name="from-right">
      <span 
        class="dish-name__second-part" 
        :style="[
          getDishNamePartStyle,
          getDishNameSecondPartStyle,
          resizeFontByNameLenght(getRestOfName)
        ]"
        :key="Math.random()"
      >          
        {{ getRestOfName }}
      </span>
    </transition>
</div>
</template>

<script>
export default {
  name: 'TheDishName',
  data() {
    return {
      baseSize: 30
    }
  },
  props: {
    listOfDishes: {
      type: Array,
      require: true
    },
    currentDishIndex: {
      type: Number,
      require: true
    }
  },
  computed: {
    getDishNameStyle() {
      return `
      height: ${this.baseSize*2}px; 
      line-height: ${this.baseSize}px;`
    },
    getDishNamePartStyle() {
      return `
      height: ${this.baseSize}px;`
    },
    getDishNameSecondPartStyle() {
      return `
      top: ${this.baseSize}px;`
    },
    getFirstPartOfName() {   
      const name = this.listOfDishes[this.currentDishIndex].name;
      const nameArray = name.split(" ");
      const halfOfname = Math.ceil(nameArray.length / 2);
      const firstHalf = nameArray.slice(0, halfOfname);
      return firstHalf.join(" ")
    }, 
    getRestOfName() {   
      const name = this.listOfDishes[this.currentDishIndex].name;
      const nameArray = name.split(" ");
      const halfOfname = Math.ceil(nameArray.length / 2);
      const secondHalf = nameArray.slice(halfOfname, nameArray.length);
      return secondHalf.join(" ")
    }
  },
  methods: {
    resizeFontByNameLenght(name) {
      const nameToResizeArray = Array.from(name);
      const letterLimit = 9;
      if (nameToResizeArray.length <= letterLimit) {
        return `font-size: ${this.baseSize}px`;
      } else if (nameToResizeArray.length > letterLimit) {
        const howMuch = nameToResizeArray.length - letterLimit;
        const decreasedSize = this.baseSize - howMuch;
        return `font-size: ${decreasedSize}px`;
      }
    }
  }
}
</script>

<style lang="scss" scoped>

.dish-name {
  text-align: left;
  width: 100%;
  position: relative;
  text-transform: uppercase;

  &__first-part, &__second-part {
    display: block;
    position: absolute;
    width: fit-content;
  }

  &__first-part {
    top: 0px;
    font-weight: 100;
  }

  &__second-part {
    font-weight: 800;
    letter-spacing: -2px;
  }
}


// from-left animation

.from-left-enter-active {
  animation: from-left-in 0.5s ease-in;
}

.from-left-leave-active {
  animation: from-left-out 0.5s ease-in;
}

.from-left-enter, .from-left-leave-to {
  opacity: 0;
}

@keyframes from-left-out {
  from { clip-path: inset(0% 0% 0% 0%) }
  to { clip-path: inset(0% 100% 0% 0%) }
}

@keyframes from-left-in {
  from { clip-path: inset(0% 100% 0% 0%) }
  to { clip-path: inset(0% 0% 0% 0%) }
}

// from-right animation

.from-right-enter-active {
  animation: from-right-in 0.5s ease-in;
}

.from-right-leave-active {
  animation: from-right-out 0.5s ease-in;
}

.from-right-enter, .from-right-leave-to {
  opacity: 0;
}

@keyframes from-right-out {
  from { clip-path: inset(0% 0% 0% 0%) }
  to { clip-path: inset(0% 0% 0% 100%) }
}

@keyframes from-right-in {
  from { clip-path: inset(0% 0% 0% 100%) }
  to { clip-path: inset(0% 0% 0% 0%) }
}

</style>