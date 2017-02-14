<template>
  <div class="main light-blue darken-3">
    <span class="intro">Welcome to Your Personal Daily Diet Tracker!
    </span>
    <div class="input-field col s6">
          <input id="icon_prefix" type="number" class="validate" v-model="goal">
          <label for="icon_prefix">Calorie Target</label>
          <a class="waves-effect waves-light btn" @click="enterGoal">Submit</a>
    </div>
  </div>
</template>

<script>
export default {

  data () {
    return {
      goal: 2000
    }
  },

  methods: {
    enterGoal () {
      this.$evt.$emit('enterGoal', {
        goal: this.goal
      })
    }
  }

}
</script>

<style scoped>
.main {
  height: 100vh;
  margin-top: 0px;
  text-align: center;
}

.intro {
  font-size: 50px;
  color: white;
  padding-top: 200px;
  padding-bottom: 50px;
  display: block;

  -webkit-animation: fadein 7s; /* Safari, Chrome and Opera > 12.1 */
     -moz-animation: fadein 7s; /* Firefox < 16 */
      -ms-animation: fadein 7s; /* Internet Explorer */
       -o-animation: fadein 7s; /* Opera < 12.1 */
          animation: fadein 7s;
}

input {
  width: 20%;
}

/* label underline focus color */
  .input-field input[type=number].valid {
    border-bottom: 1px solid white;
    box-shadow: 0 1px 0 0 white;
  }

/*label focus color*/
.input-field input[type=number]:focus + label {
     color: white;
}

/* label underline focus color */
.input-field input[type=number]:focus {
     border-bottom: 1px solid white;
     box-shadow: 0 1px 0 0 white;
}


@keyframes fadein {
    from { opacity: 0; }
    to   { opacity: 1; }
}

/* Firefox < 16 */
@-moz-keyframes fadein {
    from { opacity: 0; }
    to   { opacity: 1; }
}

/* Safari, Chrome and Opera > 12.1 */
@-webkit-keyframes fadein {
    from { opacity: 0; }
    to   { opacity: 1; }
}
</style>
