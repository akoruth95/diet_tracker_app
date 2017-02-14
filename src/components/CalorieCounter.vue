<template>
  <div class="container">
    <div class="card">
      <div class="card-content">
        <table class="centered striped">
              <thead>
                <tr>
                    <th data-field="id">Goal</th>
                    <th data-field="name">Today</th>
                    <th data-field="price">Net</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td>{{targetCalories}}</td>
                  <td>{{totalCalories}}</td>
                  <td>{{netCalories}}</td>
                </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  props: ['totalCalories', 'targetCalories'],

  data () {
    return {
      netCalories: 0
    }
  },

  methods: {
    get () {
    }
  }

}

</script>

<style scoped>
.container {
  text-align: center;
  height: 50%;
  padding-top: 10px;
  padding-bottom: 0px;
}

.card {
  border-radius: 50px;
  width: 70%;
  margin: auto;

}

</style>
