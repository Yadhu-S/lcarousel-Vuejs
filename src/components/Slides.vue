<template>
<div>
  <div class="topPrev">
    <div class="slideImg" :style="`transform:translateX(${getOffsetTop}px);`">
      <img v-for="slide in slides" :key="slide.id" class="bigImgs" :src="slide.src">
    </div>
  </div>
  <div class="bottomPrev">
    <div class="slideImg" :style="`transform:translateX(${getOffset}px);`" >
      <img v-for="(slide,index) in slides" @mouseover="prevPic(index)" :key="slide.id" class="smallImgs" :src="slide.src">
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
  computed: {
    getOffset () {
      return this.offset
    },
    getOffsetTop () {
      return this.offsetTop
    }
  },
  methods: {
    prevPic (index) {
      console.log(index)
      this.offsetTop = index * -300
    },
    moveLeft () {
      if (this.offset !== 0) {
        this.offset = this.offset + 100
      }
      if (this.offsetTop !== 0) {
        this.offsetTop = this.offsetTop + 300
      }
    },
    moveRight () {
      if (this.offset >= ((this.slides.length - 4) * -100)) {
        this.offset -= 100
      }
      if (this.offsetTop >= (this.slides.length - 2) * -300) {
        this.offsetTop -= 300
        console.log(this.offsetTop)
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
.topPrev {
  width: 300px;
  height: 300px;
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
