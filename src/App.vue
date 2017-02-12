<template>
  <div id="app">
      <div class="meal">
        <h3 class="header">Breakfast</h3>
        <span class="meal-span">
          <meal></meal>
            <a class='btn-floating btn-large waves-effect waves-light light-blue darken-3'><i class="material-icons">add</i></a>
        </span>
      </div>
      <div class="meal">
        <h3 class="header">Lunch</h3>
        <span class="meal-span">
          <a class='btn-floating btn-large waves-effect waves-light light-blue darken-3'><i class="material-icons">add</i></a>
        </span>
      </div>
      <div class="meal">
        <h3 class="header">Dinner</h3>
        <span class="meal-span">
          <a class='btn-floating btn-large waves-effect waves-light light-blue darken-3'><i class="material-icons">add</i></a>
        </span>
      </div>
</template>

<script>
import Meal from './components/Meal'
import axios from 'axios'

export default {
  name: 'app',

  components: {
    Meal
  },

  data () {
    return {
      breakfast: [],
      lunch: [],
      dinner: []
    }
  },

  mounted () {
    axios.get('/static/breakfast.json')
      .then((response) => {
        console.log(response.data)
      })
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
