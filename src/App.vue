<template>
  <div class="app">
    <Vest/>
    <Vroduct/>
  </div>
</template>

<script>
import Vest from './components/Vest'
import Vroduct from './components/Vroduct'

export default {
  name: 'app',
  components: {
    Vest,
    Vroduct
  }
}
</script>

<style>
.app {
  background-color: #eee;
}
</style>
