<template>
<div 
  class="big-screen-info" 
  v-if="windowWidth >= 560"
>
  <transition name="hideUnder">
    <div 
      v-if="isInfoVisible"
      class="big-screen-info__message"
    >
      <p>Hi. I'm a mobile app (PWA) designed to work in portrait view. Check how good I look on the screen of your smartphone. 📱</p>
      <p>Have a nice day and take care! 
        <span 
          @click="$emit('toggle-info-visibility')" 
          class="big-screen-info__hide-button"
        >
          Hide this info.
        </span>
      </p>
    </div>
  </transition>
  <transition name="hideUnder">
    <div 
      v-if="!isInfoVisible" 
      class="big-screen-info__show-button"
    >
      <img 
        @click="$emit('toggle-info-visibility')" 
        src="../assets/img/info-icon.svg" 
        class="icon"
      />
    </div>
  </transition>
</div>
 
</template>

<script>
export default {
  name: 'TheAppScaledWrapperInfoBox',
  props: {
    isInfoVisible: {
      type: Boolean,
      require: true
    },
    windowWidth: {
      type: Number,
      require: true
    }
  }
}
</script>

<style lang="scss" scoped>

.big-screen-info {
  position: absolute;
  right: 0px;
  top: 75px;
  z-index: 1;

  &__message {
    background-color: rgb(255, 255, 255);
    padding: 20px;
    width: 200px;
    position: absolute;
    right: -200px;
    font-size: 12px;
  }

  &__show-button {
    width: 200px;
    position: absolute;
    right: -200px;
    font-size: 12px;

    .icon {
      background-color: rgb(255, 255, 255);
      display: block;
      width: 24px;
      height: 24px;
      padding: 15px 15px 15px 25px;
      box-sizing: content-box;
      cursor: pointer;
    }
  }

  &__hide-button {
    text-decoration: underline;
    cursor: pointer;
  }
}


// hideUnder animation

.hideUnder-enter-active {
  animation: hideUnder-in 0.5s ease-in;
  animation-delay: 0.4s;
  opacity: 0;
}

.hideUnder-leave-active {
  animation: hideUnder-out 0.5s ease-in;
}

.hideUnder-enter, .hideUnder-leave-to {
  opacity: 0;
  right: 0px;
}

@keyframes hideUnder-out {
  from { 
    opacity: 1;
    right: -200px;
  }
  to { 
    opacity: 0;
    right: 0px;
  }
}

@keyframes hideUnder-in {
  from { 
    opacity: 0;
    right: 0px;
  }
  to { 
    opacity: 1;
    right: -200px;
  }
}

</style>
