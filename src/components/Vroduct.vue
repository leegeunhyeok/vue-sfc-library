<template>
  <div class="vroduct">
    {{ message }}
  </div>
</template>

<script>
export default {
  name: 'vroduct',
  data () {
    return {
      message: 'Vue pRODUCT'
    }
  }
}
</script>

<style>
.vroduct {
  font-size: 2rem;
  font-weight: bold;
  color: crimson;
}
</style>
