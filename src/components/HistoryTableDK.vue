<template>
  <div>
    <b-table
      :items="items"
      striped
      hover/>
  </div>
</template>

<script>
export default {
  name: 'HistoryTableDK',
  props: {
    items: {
      type: Array,
      default() {
        return []
      },
    },
  },
}
</script>

<style scoped>
</style>
