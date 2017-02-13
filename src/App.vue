<template>
  <div id="app">
      <div class="meal">
        <h3 class="header">Breakfast</h3>
        <span class="meal-span">
          <meal v-for="food in breakfast">{{food.details.item}}</meal>
          <a class='btn-floating btn-large waves-effect waves-light light-blue darken-3' @click="openModal('breakfast')"><i class="material-icons">add</i></a>
        </span>
      </div>
      <div class="meal">
        <h3 class="header">Lunch</h3>
        <span class="meal-span">
          <meal v-for="food in lunch">{{food.details.item}}</meal>
          <a class='btn-floating btn-large waves-effect waves-light light-blue darken-3' @click="openModal('lunch')"><i class="material-icons">add</i></a>
        </span>
      </div>
      <div class="meal">
        <h3 class="header">Dinner</h3>
        <span class="meal-span">
          <meal v-for="food in dinner">{{food.details.item}}</meal>
          <a class='btn-floating btn-large waves-effect waves-light light-blue darken-3' @click="openModal('dinner')"><i class="material-icons">add</i></a>
        </span>
      </div>
      <Modal v-if="showModal" @close="showModal = false" :current-meal="currentMeal"></Modal>
    </div>
</template>

<script>
import Meal from './components/Meal'
import Modal from './components/AddModal'

export default {
  name: 'app',

  components: {
    Meal,
    Modal
  },

  data () {
    return {
      showModal: false, // used to toggle modal hide and show,set to true when add button is clicked
      currentMeal: '',
      breakfast: [],
      lunch: [],
      dinner: []
    }
  },

  mounted () {
    this.$evt.$on('add', this.addMeal)
  },

  methods: {
    addMeal (data) {
      console.log(data.meal)
      if (data.meal === 'breakfast') {
        this.breakfast.push({
          item: data.selectedItem,
          details: data.foodDetails
        })
      } else if (data.meal === 'lunch') {
        this.lunch.push({
          item: data.selectedItem,
          details: data.foodDetails
        })
      } else if (data.meal === 'dinner') {
        this.dinner.push({
          item: data.selectedItem,
          details: data.foodDetails
        })
      }
    },

    openModal (whichMeal) {
      this.showModal = true
      this.currentMeal = whichMeal
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
.meal {
  padding: 50px;
}
.btn-floating {
  box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.19), 0px 6px 6px rgba(0, 0, 0, 0.23);
}
</style>
