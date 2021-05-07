<!-- 320 pixeli moznaby podać jakoś kulturalniej np. w postaci zmiennych. Podobnie jak to 560. -->

<template>
<div 
  class="wrapper"
  :style="getScaleValue"
>
  <div class="scaled-wrapper">
    <slot></slot>
  </div> 
  <TheAppScaledWrapperInfoBox 
    :isInfoVisible="isInfoVisible"
    :windowWidth="windowWidth"
    @toggle-info-visibility="toggleInfoVisibility"
  />
</div>
</template>

<script>
import TheAppScaledWrapperInfoBox from "./TheAppScaledWrapperInfobox"

export default {
  name: 'TheAppScaledWrapper',
  components: {
    TheAppScaledWrapperInfoBox
  },
  data(){
    return {
      windowWidth: window.innerWidth,
      isInfoVisible: true
    }
  },
  mounted() {
    window.addEventListener('resize', this.onResize);
  },
  beforeUnmount() { 
    window.removeEventListener('resize', this.onResize); 
  },
  computed: {
    getScaleValue () {
      if (this.windowWidth < 560) {
        let scale = (( (this.windowWidth) / (320/100)) /100);
        return `transform: scale(${scale})`
      } else {
        return ''
      }
    }
  },
  methods: {
    onResize() {
      this.windowWidth = window.innerWidth;
    },
    toggleInfoVisibility() {
      this.isInfoVisible = !this.isInfoVisible;
    }
  }
}
</script>

<style lang="scss" scoped>

.wrapper {
  position:relative;
  width: var(--base-mobile-width-size);
  height: var(--base-mobile-height-size);
  transform-origin: center;
}

.scaled-wrapper {
  width: var(--base-mobile-width-size);
  height: var(--base-mobile-height-size);
  transform-origin: center;
  position: relative;
  z-index: 2;
  
  @media screen and (min-width: 560px) {
    border: 6px solid black;
    overflow: hidden;
    margin-top: 15px;
    box-sizing: content-box;
    background: rgb(226,226,226);
    background: linear-gradient(0deg, rgba(226,226,226,1) 0%, rgba(186,186,186,1) 100%);
    box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
  }
}

</style>
