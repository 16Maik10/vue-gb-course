<template>
  <div id="app">
    <app-calc></app-calc>
  </div>
</template>

<script>
import appCalc from './components/app-calc.vue'

export default {
  name: 'App',
  components: {
    appCalc
  }
}
</script>

<style>
#app{
  display: flex;
  justify-content: center;
}
</style>
