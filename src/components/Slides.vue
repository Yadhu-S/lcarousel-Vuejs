<template>
<div>
  <div :style="`width:${topImgSize}px; height:${topImgSize}px;`" class="topPrev">
    <div class="slideImg" :style="`transform:translateX(${getOffsetTop}px);`">
      <img v-for="slide in slides" :key="slide.id" class="bigImgs" :src="slide.src">
    </div>
  </div>
  <div class="bottomPrev">
    <div class="slideImg" :style="`transform:translateX(${getOffset}px);`" >
      <img v-for="(slide,index) in slides" @mouseover="prevPic(index)" 
      @mouseout="away" @click="fixImg(index)"
      :key="slide.id" class="smallImgs" :src="slide.src">
    </div>
  </div>
  <button @click.prevent="moveLeft">Left</button>
  <button @click.prevent="moveRight">Right</button>
</div>
</template>

<script>
export default {
  data () {
    return {
      offset: 0,
      offsetTop: 0,
      temp: 0,
      mvLft: false,
      slides: [
        {src: '../../static/1.jpg'},
        {src: '../../static/2.jpg'},
        {src: '../../static/3.jpg'},
        {src: '../../static/4.jpg'},
        {src: '../../static/5.jpg'},
        {src: '../../static/6.jpg'},
        {src: '../../static/7.jpg'}
      ]
    }
  },
  props: {
    topImgSize: {
      type: Number,
      default: 300
    }
  },
  computed: {
    getOffset () {
      if (this.offset <= -300 || this.mvLft) {
        this.mvLft = false
        return this.offset
      }
      console.log(this.mvLft)
    },
    getOffsetTop () {
      return this.offsetTop
    }
  },
  methods: {
    // Called when mouse moves away
    away () {
      this.offsetTop = this.temp
    },
    // Called when mouse hovers
    prevPic (index) {
      this.temp = this.offsetTop
      this.offsetTop = index * -this.topImgSize
    },
    // Called when clicked on image
    fixImg (index) {
      this.offsetTop = index * -this.topImgSize
      this.temp = this.offsetTop
    },
    // Called when left button is clicked
    moveLeft () {
      if (this.offset !== 0) {
        this.offset = this.offset + 100
      }
      if (this.offsetTop !== 0) {
        this.offsetTop = this.offsetTop + this.topImgSize
      }
      this.mvLft = true
    },
    // Called when right button is clicked
    moveRight () {
      if (this.offset >= ((this.slides.length - 4) * -100)) {
        this.offset -= 100
      }
      if (this.offsetTop >= (this.slides.length - 2) * -this.topImgSize) {
        this.offsetTop -= this.topImgSize
      }
    }
  }
}
</script>

<style scoped>
.bottomPrev,.topPrev{
  width:300px;
  height: 100px;
  background-color: gray;
  overflow: hidden;
}
.smallImgs,.bigImgs{
  width:100px;
  height: 100px;
  flex: 1 0 auto;
}
.bigImgs {
  width: 300px;
  height: 300px;
}
.smallImgs{
  cursor: pointer;
}
.slideImg{
  display: flex;
}
</style>
