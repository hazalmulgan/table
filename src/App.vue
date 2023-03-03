<template>
  <div id="app">
    <CarTable/>
  </div>
</template>

<script>
import CarTable from './components/CarTable.vue'

export default {
  name: 'App',
  components: {
    CarTable
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 60px;
}
</style>
