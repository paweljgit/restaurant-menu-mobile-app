<template>
<div class="order">
    <div class="price">
      <img 
        src="../assets/img/money-icon.svg"
        class="order__icon"
        alt="price icon"
      />
      <div class="price">
        <transition name="fade">
          <span 
            class="price__value" 
            :key="Math.random()"
          >
            {{ getCurrentDishPrice }} $
          </span>
        </transition>
      </div>
    </div>
    <div class="addToCart">
      <img 
        src="../assets/img/ringbell-icon.svg" 
        class="order__icon"
        alt="order icon"
      />
      <button 
        class="addToCartButton" 
        @click="modalToggle"
      >
        Add to cart
      </button>
    </div>
    <transition name="fade">
      <Modal 
        v-if="isModalVisible" 
        @close-modal="modalToggle"
      />
    </transition>
</div>
</template>

<script>
import Modal from './Modal'

export default {
  name: 'TheDishOrder',
  components: {
   Modal
  },
  data() {
    return {
      isModalVisible: false
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
    getCurrentDishPrice () {
      return this.listOfDishes[this.currentDishIndex].price
    }
  },
  methods: {
    modalToggle() {
      this.isModalVisible = !this.isModalVisible
    }
  }
}
</script>

<style lang="scss" scoped>

.order {
  position: relative;
  width: 100%;
  padding: 5px 0px;
  margin: 10px 0px;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;

  &__icon {
    margin-right: 10px;
    height: 20px;
    width: 20px;
  }

  .price, .addToCart {
    width: 50%;
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    position: relative;
  }

  .price__value {
    position: absolute;
    top: 0px;
  }

  .addToCartButton {
    background-color: transparent;
    border: none;
    padding: 0px;
    margin: 0px;
    display: flex;
    cursor: pointer;
    font-size: 100%;
  }
}


// fade animation

.fade-enter-active {
  animation: fade-in 0.5s ease-in;
}

.fade-leave-active {
  animation: fade-out 0.5s ease-in;
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