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
      foods: [],
      selected: 'Search',
      foodDetails: null,
      counter: 0
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
    filteredFoods: function () {
      return this.foods.filter((food) => {
        if (this.selected !== '') {
          return food.item.toUpperCase().includes(this.selected.toUpperCase())
        }
      })
    }
  },

  methods: {
    select (item) {
      this.selected = item
    },
    add () {
      if (this.selected !== '') {
        for (this.counter = 0; this.counter < this.foods.length; this.counter++) {
          if (this.foods[this.counter].item === this.selected) {
            this.foodDetails = this.foods[this.counter]
            console.log(this.foodDetails)
            break
          }
        }
        console.log('hello: ', this.selectedItem)
        this.$evt.$emit('add', {
          selectedItem: this.selected,
          foodDetails: this.foodDetails,
          meal: this.currentMeal
        })
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
