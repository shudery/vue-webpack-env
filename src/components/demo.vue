<template>
  <div class="container">
    <div ref="slides" class="slides"> 
      <div v-if="currentIndex" class="pre-slide slide" :style="{backgroundColor:slides[currentIndex-1].color}">
          <p>{{slides[currentIndex-1].content}}</p>
      </div>
      <div class="cur-slide slide" :style="{backgroundColor:slides[currentIndex].color}">
          <p>{{slides[currentIndex].content}}</p>
      </div>

      <div ref="nextSlide" v-if="currentIndex < slides.length-1" class="next-slide slide" :style="{backgroundColor:slides[currentIndex+1].color}">
          <p>{{slides[currentIndex+1].content}}</p>
      </div>
    </div>
    <div class="btn">
      <button @click="nextSlide(1)"><</button>
      <button @click="nextSlide(-1)">></button>
    </div>
  </div>
</template>
<style >
.slide {
  height: 100px;
  width: 200px;
  margin: 0 auto;
  float: left;
}
/* .view{
    width:220px;
    height:100px;
} */
/* .pre-slide {
  display: none;
}
.next-slide {
  display: none;
} */
/* .cur-slide { */
/* position: absolute;
  left: 200px; */
/* } */
.slides {
  position: relative;
  z-index: 2;
  background-color: aqua;
  width: 600px;
  margin: 0 auto;
}
.btn {
  clear: left;
}
</style>

<script>
export default {
  data() {
    return {
      animateIng: false,
      currentIndex: 1,
      slides: [
        { id: 0, content: "slides 0", color: "#fff" },
        { id: 1, content: "slides 1", color: "red" },
        { id: 2, content: "slides 2", color: "orange" },
        { id: 3, content: "slides 3", color: "yellow" },
        { id: 4, content: "slides 4", color: "grey" },
        { id: 5, content: "slides 5", color: "green" },
        { id: 6, content: "slides 6", color: "blue" },
        { id: 7, content: "slides 7", color: "#fff" }
      ]
    };
  },
  methods: {
    nextSlide(type) {
      //边界判断
      if (
        (type === -1 && this.currentIndex === this.slides.length - 2) ||
        (type === 1 && this.currentIndex === 1)
      )
        return console.log("slide to end/start now");
      //判断是否正在slide切换中
      if (!this.animateIng) {
        this.animateIng = true;
        this.$refs.slides.animate(
          [
            { transform: "translateX(0)" },
            { transform: "translateX(" + type * 200 + "px)" }
          ],
          {
            duration: 300,
            iteration: 1,
            easing: "ease"
          }
        ).onfinish = () => {
          //动画执行完，刷新数据
          this.animateIng = false;
          this.currentIndex = this.currentIndex - type;
        };
      } else {
        console.log("click unwork,slide animate is running.");
      }
    }
  }
};
</script>
