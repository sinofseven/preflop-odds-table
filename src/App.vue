<template>
  <div id="app">
    <div class="container">
      <b-navbar class="navbar-expand-sm" toggleable="lg" type="dark" :sticky="true" variant="primary">
        <b-navbar-brand>Preflop Odds</b-navbar-brand>
        <b-navbar-nav class="ml-auto">
          <b-button-group>
          <b-button button href="#app" variant="primary" class="d-inline-block" v-smooth-scroll>
            <font-awesome-icon icon="long-arrow-alt-up" size="2x" style="color: white" />
          </b-button>
          <b-button v-b-modal.config variant="primary" class="d-inline-block">
            <font-awesome-icon icon="cog" size="2x" style="color: white" />
          </b-button>
          </b-button-group>
        </b-navbar-nav>
      </b-navbar>
      <b-modal scrollable id="config" ref="config" title="config" @ok="handleOk" @hide="restoreForm">
        <b-form-group label="">
          <b-form-radio-group
            v-model="formValues.isRate"
            :options="formOptions.isRate"
          />
        </b-form-group>
        <hr />
        <b-form-group label="Filter">
          <b-form-checkbox inline v-model="formValues.visiblePocket">Pocket</b-form-checkbox>
          <b-form-checkbox inline v-model="formValues.visibleSuited">Suited</b-form-checkbox>
          <b-form-checkbox inline v-model="formValues.visibleOffSuit">Off Suit</b-form-checkbox>
        </b-form-group>
        <hr />
        <b-form-group label="Rate Threshold">
          <b-form-select v-model="formValues.threshold" :options="formOptions.threshold" />
        </b-form-group>
        <hr />
        <b-form-group label="Players">
          <b-form-select v-model="formValues.players" :options="formOptions.players" />
        </b-form-group>
      </b-modal>
      <odds-table
        :players="players"
        :preflopOdds="preflopOdds"
        :threshold="threshold"
        :visiblePocket="visiblePocket"
        :visibleSuited="visibleSuited"
        :visibleOffSuit="visibleOffSuit"  
        :isRate="isRate"      
      ></odds-table>
    </div>
  </div>
</template>

<script>
import OddsTable from "./components/OddsTable.vue"
import PreflopOdds from "./preflop_odds"
export default {
  name: "app",
  data() {
    return {
      players: 4,
      preflopOdds: PreflopOdds,
      threshold: 0,
      isRate: true,
      visiblePocket: true,
      visibleSuited: true,
      visibleOffSuit: true,
      formValues: {
        players: 4,
        threshold: 0,
        visiblePocket: true,
        visibleSuited: true,
        visibleOffSuit: true,
        isRate: true
      },
      formOptions: {
        threshold: [
          {text: '0%', value: 0},
          {text: '10%', value: 10},
          {text: '20%', value: 20},
          {text: '30%', value: 30},
          {text: '40%', value: 40},
          {text: '50%', value: 50},
          {text: '60%', value: 60},
          {text: '70%', value: 70},
          {text: '80%', value: 80},
          {text: '90%', value: 90}
        ],
        players: [
          {text: '2 players', value: 2},
          {text: '3 players', value: 3},
          {text: '4 players', value: 4},
          {text: '5 players', value: 5},
          {text: '6 players', value: 6},
          {text: '7 players', value: 7},
          {text: '8 players', value: 8},
          {text: '9 players', value: 9},
          {text: '10 players', value: 10}
        ],
        isRate: [
          {text: 'rate', value: true},
          {text: 'times', value: false}
        ]
      }
    }
  },
  methods: {
    handleOk(bvModalEvt) {
      for(const key of Object.keys(this.formValues)) {
        this[key] = this.formValues[key];
      }
    },
    restoreForm() {
      for(const key of Object.keys(this.formValues)) {
        this.formValues[key] = this[key];
      }
    },
    toTop(bvModalEvt) {
      bvModalEvt.preventDefault();
      $('html, body').animate({ scrollTop: 0 }, 'slow');
    }
  },
  components: {
    OddsTable
  }
};
</script>

<style>
select {
  display: inline-block;
}
</style>
