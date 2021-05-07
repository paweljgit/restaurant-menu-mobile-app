<template>
<div :class="[
    'item',
    [index === currentDishIndex ? 'item--current' : '']
  ]"
>
  <div 
    :style="getDishPictureStyle" 
    class="item__picture"
  ></div>
  <span class="item__name">{{ dish.name }}</span>
</div>
</template>

<script>
export default {
  name: 'NavigationItem',
  props: {
    dish: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    },
    currentDishIndex: {
      type: Number,
      required: true
    }
  },
  computed: {
    getDishPictureStyle () {
      return `background-image: url("${this.dish.pic}");`
    }
  } 
}
</script>

<style lang="scss" scoped>

.item {
  height: 115px;
  width: 70px;
  padding: 5px 10px 10px 10px;
  margin-right: 15px;
  border-radius: 7px;
  overflow: hidden;
  cursor: pointer;
  font-size: 12px;
  display: flex;
  flex-direction: column;
  align-items: center;

  &__picture {
    min-width: 50px;
    min-height: 50px;
    max-width: 50px;
    max-height: 50px;
    margin-bottom: 5px;
    background-size: cover;
    background-position: 50% 50%;
  }

  &__name {
    display: flex;
    width: 100%;
    flex-grow: 1;
    text-align: center;
    justify-content: center;
    align-items: top;
    font-weight: 200;
    line-height: 125%;
  }
  
  &--current {
    box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 12px;
    transition: all 0.5s ease-in-out 0.5s;
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