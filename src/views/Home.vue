<template>
  <div class="home">
    <nav-bar />
    <b-jumbotron
      header="Bootstrap Vue"
      lead="Bootstrap 4 Components for Vue.js 2" >
      <p>For more information visit website</p>
      <b-btn-group size="lg">
        <b-btn variant="primary">Entries {{ entries }}</b-btn>
        <b-btn variant="info">Fees Paid ${{ feesPaid | currency }}</b-btn>
        <b-btn variant="success">Profit ${{ profit | currency }}</b-btn>
        <b-btn variant="success">ROI {{ profit | currency }}%</b-btn>
      </b-btn-group>
    </b-jumbotron>
    <history-table-d-k :items="data" />
  </div>
</template>

<script>
const data = [
  { id: 1, contestName: 'NFL Pylon 9000', won: 0, entryFee: 1.0 },
  { id: 2, contestName: 'NFL Spike 2k', won: 1.8, entryFee: 1.0 },
  { id: 3, contestName: 'NFL Huddle', won: 5.0, entryFee: 1.0 },
  { id: 4, contestName: 'NFL Smash', won: 2.6, entryFee: 2.0 },
  { id: 5, contestName: 'NFL Spike', won: 0, entryFee: 2.0 },
  { id: 6, contestName: 'NFL Gauntlet', won: 0, entryFee: 1.0 },
  { id: 7, contestName: 'NFL Oklahoma Drill', won: 1.8, entryFee: 1.0 },
  { id: 8, contestName: 'NFL H2H', won: 0, entryFee: 1.0 },
  { id: 9, contestName: 'NFL 50/50', won: 0, entryFee: 1.0 },
]
import NavBar from '@/components/BaseNavBar.vue'
import HistoryTableDK from '@/components/HistoryTableDK.vue'

export default {
  name: 'Home',
  components: {
    NavBar,
    HistoryTableDK,
  },
  filters: {
    currency(value) {
      if (!value || value === 0) return

      return value.toFixed(2)
    },
  },
  data() {
    return {
      data,
    }
  },
  computed: {
    entries() {
      return data.length
    },
    feesPaid() {
      return data.reduce((accum, item) => (accum += item.entryFee), 0)
    },
    profit() {
      return data.reduce((accum, item) => (accum += item.won), 0) - this.feesPaid
    },
    roi() {
      return (this.profit / this.feesPaid) * 100
    },
  },
}
</script>
