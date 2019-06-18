<template>
  <div class="vest">
    {{ message }}
  </div>
</template>

<script>
export default {
  name: 'vest',
  data () {
    return {
      message: 'Vue tEST'
    }
  }
}
</script>

<style>
.vest {
  font-size: 2rem;
  font-weight: bold;
  color: cornflowerblue;
}
</style>
