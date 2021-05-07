<template>
<div class="dish-info">
  <TheDishName
    :listOfDishes="listOfDishes"
    :currentDishIndex="currentDishIndex"
  />
  <TheDishOrder
    :listOfDishes="listOfDishes"
    :currentDishIndex="currentDishIndex"
  />
  <TheDishDescription 
    :listOfDishes="listOfDishes"
    :currentDishIndex="currentDishIndex"
  />
</div>
</template>

<script>
import TheDishName from './TheDishName'
import TheDishOrder from './TheDishOrder'
import TheDishDescription from './TheDishDescription'

export default {
  name: 'TheDishInfo',
  components: {
   TheDishName, TheDishOrder, TheDishDescription
  },
  props: {
    listOfDishes: {
      type: Array,
      require: true
    },
    currentDishIndex: {
      type: Number,
      require: true
    },
    dish: {
      type: Object,
      require: true
    }
  }
}
</script>

<style lang="scss" scoped>

.dish-info {
  margin-top: -85px;
  padding: 0px var(--mobile-x-padding);
  animation: simplyFade 0.5s ease-out;
  animation-delay: 0.8s;
  animation-fill-mode: forwards;
  opacity:0;
}

@keyframes simplyFade {
  from {
    opacity:0;
  }
  to {
    opacity:1;
  }
}

</style>
