<template>
  <cars-table></cars-table>
</template>

<script>
import CarsTable from './components/CarsTable.vue'

export default {
  name: 'App',
  components: {
    CarsTable
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.sr-only{
  display: none;
}
</style>
