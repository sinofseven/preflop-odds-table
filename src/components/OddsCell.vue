<template>
  <td v-bind:class="{under: is_under}" class="text-center">{{ to_text }}</td>
</template>

<script>
export default {
  name: "OddsCell",
  props: {
    rate: Number,
    threshold: Number,
    isRate: Boolean
  },
  computed: {
    is_under: function() {
      return this.rate < this.threshold; 
    },
    to_text: function() {
      if (this.isRate) {
        return `${this.rate.toFixed(1)}%`
      } else {
        return `${(100 / this.rate).toFixed(1)}`
      }
    }
  }
}
</script>

<style>
td.under {
  background-color: gray
}
</style>
