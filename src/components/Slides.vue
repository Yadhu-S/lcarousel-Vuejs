<template>
<div>
  <div :style="`width:${topImgSize}px; height:${topImgSize}px;`" class="topPrev">
    <div class="slideImg" :style="`transform:translateX(${getOffsetTop}px);`">
      <div v-for="slide in slides" :key="slide.id" class="bigImgCont">
        <img class="bigImgs" :src="slide.src">
      </div>
    </div>
  </div>
  <i @click="moveLeft" class="fa fa-angle-left" id="leftArrow" aria-hidden="true"></i>
  <i @click="moveRight"class="fa fa-angle-right" id="rightArrow" aria-hidden="true"></i>
  <div class="bottomPrev">
    <div class="slideImg" :style="`transform:translateX(${getOffset}px);`" >
      <div v-for="(slide,index) in slides" :key="slide.id" class="smallImgCont">
        <img @mouseover="prevPic(index)" 
        @mouseout="away" @click="fixImg(index)"
        class="smallImgs" :src="slide.src">
      </div>
    </div>
  </div>
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
        {src: '../../../static/1.jpg'},
        {src: '../../../static/2.jpg'},
        {src: '../../../static/3.jpg'},
        {src: '../../../static/4.jpg'},
        {src: '../../../static/5.jpg'},
        {src: '../../../static/6.jpg'},
        {src: '../../../static/7.jpg'}
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
.smallImgCont,.bigImgCont{
  background-color: white;
  display: inline-block;
  margin: 0px;
  width: 100px;
  height: 80px;
  line-height: 77px;
  text-align: center;
}
#leftArrow,#rightArrow{
  cursor: pointer;
  margin-left: -14px;
  margin-top: -176px;
  position: absolute;
  font-size: 44px;
}
#rightArrow{
  float: right;
  margin-left: 292px
}
.bigImgCont{
  width: 300px;
  height: 300px;
}
.smallImgCont:hover {
  box-shadow: 4px 3px 6px 0px rgba(244, 97, 80, 0.85);
}
.smallImgCont:active {
  box-shadow: 4px 3px 6px 0px rgba(244, 97, 80, 0.85);
}
.bottomPrev,.topPrev{
  width:300px;
  height: 100px;
  overflow: hidden;
}
.smallImgs{
  width:100px;
  height: auto;
}
.bigImgs {
  max-width:100%;
  max-height:100%;
  vertical-align: middle;
}
.smallImgs{
  cursor: pointer;
  max-width:98%;
  max-height:98%;
  vertical-align: middle;
}
.smallImgs:hover{
  max-width: 100%;
  max-height: 100%;
}
.slideImg{
  display: inline-block;
  white-space: nowrap;
}
</style>
