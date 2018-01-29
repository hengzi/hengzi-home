<template>
  <div class="home">
    <canvas ref="canvas" width="825" height="803"></canvas>
    <div id="wrapper">
      <h2>Hengzi</h2>
      <h4>Discover a larger front-end.</h4>
      <p>
        <a href="https://hengzi.github.io/" target="_blank">Blog</a>
      </p>
      <p>
        <a href="https://github.com/hengzi" target="_blank">Github</a>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
      x: null,
      w: 825,
      h: 803,
      f: 60,
      q: null,
      r: 0
    }
  },
  methods: {
    i () {
      this.x.clearRect(0, 0, this.w, this.h)
      this.q = [
        { x: 0, y: this.h * 0.5 + this.f },
        { x: 0, y: this.h * 0.5 - this.f }
      ]
      while (this.q[1].x < this.w + this.f) {
        this.d(this.q[0], this.q[1])
      }
    },
    d (i, j) {
      this.x.beginPath()
      this.x.moveTo(i.x, i.y)
      this.x.lineTo(j.x, j.y)
      let k = j.x + (Math.random() * 2 - 0.25) * this.f
      let n = this.y(j.y)
      this.x.lineTo(k, n)
      this.x.closePath()
      this.r -= Math.PI * 2 / -50
      this.x.fillStyle =
        '#' +
        (
          ((Math.cos(this.r) * 127 + 128) << 16) |
          ((Math.cos(this.r + Math.PI * 2 / 3) * 127 + 128) << 8) |
          (Math.cos(this.r + Math.PI * 4 / 3) * 127 + 128)
        ).toString(16)
      this.x.fill()
      this.q[0] = this.q[1]
      this.q[1] = { x: k, y: n }
    },
    y (p) {
      var t = p + (Math.random() * 2 - 1.1) * this.f
      return t > this.h || t < 0 ? this.y(p) : t
    }
  },
  mounted () {
    let pr = window.devicePixelRatio || 1
    this.w = window.innerWidth
    this.h = window.innerHeight

    let c = this.$refs.canvas
    c.width = this.w * pr
    c.height = this.h * pr

    this.x = c.getContext('2d')
    this.x.scale(pr, pr)
    this.x.globalAlpha = 0.6

    document.addEventListener('touchmove', function (e) {
      e.preventDefault()
    })
    document.onclick = () => this.i()
    document.ontouchstart = () => this.i()
    this.i()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#wrapper {
  position: absolute;
  left: 0;
  width: 400px;
  text-align: center;
  top: 50%;
  left: 50%;
  margin-left: -200px;
  margin-top: -160px;
  -webkit-user-select: none;
  -moz-user-select: none;
  user-select: none;
}
canvas {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 0;
  width: 100%;
  height: 100%;
  /* pointer-events: none; */
}
</style>
