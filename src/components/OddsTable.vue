<template>
  <table class="table">
    <thead>
      <tr>
        <td></td>
        <th v-if="players >= 2" scope="col" class="text-center">2 players</th>
        <th v-if="players >= 3" scope="col" class="text-center">3 players</th>
        <th v-if="players >= 4" scope="col" class="text-center">4 players</th>
        <th v-if="players >= 5" scope="col" class="text-center">5 players</th>
        <th v-if="players >= 6" scope="col" class="text-center">6 players</th>
        <th v-if="players >= 7" scope="col" class="text-center">7 players</th>
        <th v-if="players >= 8" scope="col" class="text-center">8 players</th>
        <th v-if="players >= 9" scope="col" class="text-center">9 players</th>
        <th v-if="players >= 10" scope="col" class="text-center">10 players</th>
      </tr>
    </thead>
    <tbody>
      <template v-for="(rates, hand) in preflopOdds">
        <odds-row
          v-bind:key="hand"
          :hand="hand"
          :rates="rates"
          :threshold="threshold"
          :players="players"
          :visiblePocket="visiblePocket"
          :visibleSuited="visibleSuited"
          :visibleOffSuit="visibleOffSuit"
          :isRate="isRate"
        ></odds-row>
      </template>
    </tbody>
  </table>
</template>

<script>
import OddsRow from "./OddsRow.vue"
export default {
  name: "OddsTable",
  components: {
    OddsRow
  },
  props: {
    players: Number,
    preflopOdds: Object,
    threshold: Number,
    visiblePocket: Boolean,
    visibleSuited: Boolean,
    visibleOffSuit: Boolean,
    isRate: Boolean
  }
};
</script>

<style scoped>

th {
  text-align: center;
}
</style>
