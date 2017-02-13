<template>
  <div class="food">
      <div class="card">
        <div class="card-content">
          <slot></slot>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  data () {
    return {

    }
  },
  methods: {

  }
}
</script>

<style>
  .card {
    box-shadow: 0px 14px 28px rgba(0, 0, 0, 0.25), 0px 10px 10px rgba(0, 0, 0, 0.22);
  }
</style>
