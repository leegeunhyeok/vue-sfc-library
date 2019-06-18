<template>
  <div class="app">
    <Vest/>
  </div>
</template>

<script>
import Vest from './components/Vest'

export default {
  name: 'app',
  components: {
    Vest
  }
}
</script>

<style>
.app {
  background-color: #eee;
}
</style>
