<template>
  <div class="vroduct" :style="{ backgroundColor: currentColor }">
    {{ message }}
  </div>
</template>

<script>
export default {
  name: 'vroduct',
  data () {
    return {
      message: 'Vue pRODUCT',
      loop: null,
      colorList: [
        'red',
        'orange',
        'yellow',
        'green',
        'blue',
        'navy',
        'purple'
      ],
      currentColor: 'red'
    }
  },
  created () {
    this.loop = setInterval(this.changeColor, 500)
  },
  beforeDestroy () {
    clearInterval(this.loop)
  },
  methods: {
    changeColor () {
      let idx = this.colorList.indexOf(this.currentColor)
      if (idx + 1 === this.colorList.length) {
        idx = -1
      }
      this.currentColor = this.colorList[++idx]
    }
  }
}
</script>

<style lang="scss">
$duration: .3s;

.vroduct {
  font-size: 2rem;
  font-weight: bold;
  -webkit-transition: $duration;
     -moz-transition: $duration;
      -ms-transition: $duration;
       -o-transition: $duration;
          transition: $duration;
}
</style>
