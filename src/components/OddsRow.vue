<template>
  <tr v-if="isVisible">
    <th scope="row" class="text-center">{{ hand }}</th>
    <odds-cell v-if="players >= 2" :isRate="isRate" :rate="rates[0]" :threshold="threshold"></odds-cell>
    <odds-cell v-if="players >= 3" :isRate="isRate" :rate="rates[1]" :threshold="threshold"></odds-cell>
    <odds-cell v-if="players >= 4" :isRate="isRate" :rate="rates[2]" :threshold="threshold"></odds-cell>
    <odds-cell v-if="players >= 5" :isRate="isRate" :rate="rates[3]" :threshold="threshold"></odds-cell>
    <odds-cell v-if="players >= 6" :isRate="isRate" :rate="rates[4]" :threshold="threshold"></odds-cell>
    <odds-cell v-if="players >= 7" :isRate="isRate" :rate="rates[5]" :threshold="threshold"></odds-cell>
    <odds-cell v-if="players >= 8" :isRate="isRate" :rate="rates[6]" :threshold="threshold"></odds-cell>
    <odds-cell v-if="players >= 9" :isRate="isRate" :rate="rates[7]" :threshold="threshold"></odds-cell>
    <odds-cell v-if="players >= 10" :isRate="isRate" :rate="rates[8]" :threshold="threshold"></odds-cell>
  </tr>
</template>

<script>
import OddsCell from "./OddsCell.vue"
export default {
  name: "OddRow",
  components: {OddsCell},
  props: {
    hand: String,
    rates: Array,
    threshold: Number,
    players: Number,
    visiblePocket: Boolean,
    visibleSuited: Boolean,
    visibleOffSuit: Boolean,
    isRate: Boolean
  },
  computed: {
    isVisible: function() {
      if(this.visibleSuited && this.visibleOffSuit && this.visiblePocket) {
        return true;
      }
      if (this.visiblePocket && this.hand[0] === this.hand[1]) return true;
      if (!this.visiblePocket && this.hand[0] === this.hand[1]) return false;
      if (this.visibleSuited && this.hand[2] === 's') return true;
      if (this.visibleOffSuit && this.hand[2] === 'o') return true;
      return false;
    }
  }
}
</script>

<style>

</style>
