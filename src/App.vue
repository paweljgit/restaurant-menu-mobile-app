<!-- https://pin.it/7kt62xU -->

<template>
<div id="app">
  <TheAppScaledWrapper>
    <TheCarousel 
      :listOfDishes="listOfDishes"
      :currentDishIndex="currentDishIndex"
      :previousDishIndex="previousDishIndex"
      @item-swiped="itemSwiped"
    />
    <TheDish 
      :listOfDishes="listOfDishes"
      :currentDishIndex="currentDishIndex"
    />
    <TheNavigation 
      :listOfDishes="listOfDishes"
      :currentDishIndex="currentDishIndex"
      @change-current-index="changeCurrentIndex"
    />
  </TheAppScaledWrapper>
</div>
</template>

<script>
import TheAppScaledWrapper from './components/TheAppScaledWrapper'
import TheCarousel from './components/TheCarousel'
import TheDish from './components/TheDish'
import TheNavigation from './components/TheNavigation'


export default {
  name: 'App',
  components: {
   TheAppScaledWrapper, TheCarousel, TheDish, TheNavigation
  },
  data() {
    return {
      listOfDishes: [
        {
          name: 'Chicken Pakora',
          pic: 'https://s08.pl/git/img/foodro/danie.png',
          price: 12.99,
          description: 'Kawałki piersi kurczaka w panierce z ciecierzycy, podawane z sosem tamaryndowym i miętowym.'
        },
        {
          name: 'Mutton Samosa',
          pic: 'https://s08.pl/git/img/foodro/danie2.png',
          price: 19.50,
          description: 'Chrupiące pierożki z nadzieniem z mielonej baraniny i ziarnami granatu, podawane z sosem tamaryndowym i miętowym.'
        },
        {
          name: 'Tom Kha Galang z kurczakiem',
          pic: 'https://s08.pl/git/img/foodro/danie3.png',
          price: 9.00,
          description: 'Pikantno-kwaśna tajska zupa galangalowo kokosowa z dodatkiem trawy cytrynowej.'
        },
        {
          name: 'Chicken Pakora',
          pic: 'https://s08.pl/git/img/foodro/danie.png',
          price: 12.99,
          description: 'Kawałki piersi kurczaka w panierce z ciecierzycy, podawane z sosem tamaryndowym i miętowym.'
        },
        {
          name: 'Mutton Samosa',
          pic: 'https://s08.pl/git/img/foodro/danie2.png',
          price: 19.50,
          description: 'Chrupiące pierożki z nadzieniem z mielonej baraniny i ziarnami granatu, podawane z sosem tamaryndowym i miętowym.'
        },
        {
          name: 'Tom Kha Galang z kurczakiem',
          pic: 'https://s08.pl/git/img/foodro/danie3.png',
          price: 9.00,
          description: 'Pikantno-kwaśna tajska zupa galangalowo kokosowa z dodatkiem trawy cytrynowej.'
        },
        {
          name: 'Chicken Pakora',
          pic: 'https://s08.pl/git/img/foodro/danie.png',
          price: 12.99,
          description: 'Kawałki piersi kurczaka w panierce z ciecierzycy, podawane z sosem tamaryndowym i miętowym.'
        },
        {
          name: 'Mutton Samosa',
          pic: 'https://s08.pl/git/img/foodro/danie2.png',
          price: 19.50,
          description: 'Chrupiące pierożki z nadzieniem z mielonej baraniny i ziarnami granatu, podawane z sosem tamaryndowym i miętowym.'
        },
        {
          name: 'Tika Masala Que',
          pic: 'https://s08.pl/git/img/foodro/danie3.png',
          price: 9.00,
          description: 'Pikantno-kwaśna tajska zupa galangalowo kokosowa z dodatkiem trawy cytrynowej.'
        }    
        ],
      currentDishIndex: 0,
      previousDishIndex: 0,
    }
  },
  methods: {
    changeCurrentIndex(value) {
      this.previousDishIndex = this.currentDishIndex;
      this.currentDishIndex = value;
    },
    renemberPreviousDish() {
      this.previousDishIndex = this.currentDishIndex;
    },
    itemSwiped(direction) {
      if (direction === 'left') {
        this.renemberPreviousDish;

        if (this.currentDishIndex != 0) {
          this.currentDishIndex--;
        } else {
          this.currentDishIndex = this.listOfDishes.length-1;
        }

      } else {
        this.renemberPreviousDish;
        
        if (this.currentDishIndex != (this.listOfDishes.length-1)) {
          this.currentDishIndex++;
        } else {
          this.currentDishIndex = 0;
        }
      }
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@100;200;400;800&display=swap');

* {
  box-sizing: border-box;
  -webkit-tap-highlight-color: transparent;
}

html, body {
  height: 100vh;
  width: 100vw;
  margin: 0px;
  padding: 0px;
  overflow: hidden;
}

body {
  font-family: 'Poppins', Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  font-size: 14px;
  align-items: center;
  justify-content: center;
  background: rgb(226,226,226);
  background: linear-gradient(0deg, rgba(226,226,226,1) 0%, rgba(186,186,186,1) 100%);
}

button {
  font-family: 'Poppins', Arial, sans-serif;
  font-weight: 400;
}

:root {
  --base-mobile-width-size: 320px;
  --base-mobile-height-size: 569px;
  --mobile-mockup-size: 320px;
  --mobile-x-padding: 20px;
}

</style>
