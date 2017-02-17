<template>
  <div>
    <input type="text" name="search" v-model="selected">
    <!--<div class = "results">-->
    <div class="collection">
      <div class="collection-item" v-for="food in filteredFoods" @click="select(food.item)"><a class="foodItem">{{food.item}}<br /><span>{{food.calories}} calories</span></a></div>
    </div>
      <a class="waves-effect waves-light btn light-blue darken-3" @click="add">Add</a>
    <!--</div>-->
  </div>
</template>

<script>
import axios from 'axios'

export default {
  props: ['currentMeal'],

  data () {
    return {
      foods: [], // to contain all json objects
      selected: 'Search', // placeholder for search inpu
      foodDetails: null, // part of json object
      counter: 0,
      validItem: false // toggles on item click
    }
  },

  mounted () {
    axios.get('/static/breakfast.json')
      .then((response) => {
        this.foods = response.data.food
        // console.log(this.foodlist)
      })
  },

  computed: {
    filteredFoods: function () { // filter to provide live search
      return this.foods.filter((food) => {
        if (this.selected !== '') {
          return food.item.toUpperCase().includes(this.selected.toUpperCase())
        }
      })
    }
  },

  methods: {
    select (item) { // item is food item clicked on after search
      this.selected = item
      this.validItem = true
    },
    add () { // this function searches through json aray of objects and retrieves the selected food object
      if (this.validItem) {
        for (this.counter = 0; this.counter < this.foods.length; this.counter++) {
          if (this.foods[this.counter].item === this.selected) {
            this.foodDetails = this.foods[this.counter] // foodDetails is food item/object to be pushed into meal array in App.vue
            console.log(this.foodDetails)
            break
          }
        }
        this.$evt.$emit('add', {
          selectedItem: this.selected,
          foodDetails: this.foodDetails,
          meal: this.currentMeal // to indicate which meal array to be pushed into
        })
        this.validItem = false
      }
    }
  }

}
</script>

<style scoped>

.foodItem {
  color: black;
  cursor: pointer;
}

.collection:empty {
  border: none;
}

.active-collection {
  background-color: blue;
}

.collection-item:hover {
  background-color: #e6e6e6;
  cursor: pointer;
}

 .input[type=text] {
     width: 130px;
     -webkit-transition: width 0.4s ease-in-out;
     transition: width 0.4s ease-in-out;
 }

 /* When the input field gets focus, change its width to 100% */
 input[type=text]:focus {
     width: 100%;
 }
</style>
