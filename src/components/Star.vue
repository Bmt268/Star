<template>
  <div class="stars">
    <div
      v-for="(item, index) in starsCount"
      :key="index"
      class="star"
      ref="starr"
    ></div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
export default {
  name: "Star",
  data() {
    return {
      starsCount: 800, //星星数量
      distance: 800, //间距
    };
  },
  setup() {
    const starr = ref();
    onMounted(() => {
      let starArr = starr.value;
      console.log("starArr");
      starArr.forEach((item) => {
        var speed = 0.2 + Math.random() * 1;
        var thisDistance = this.distance + Math.random() * 300;
        item.style.transformOrigin = `0 0 ${thisDistance}px`;
        item.style.transform = `translate3d(0,0,-${thisDistance}px) rotateY(${
          Math.random() * 360
        }deg) rotateX(${Math.random() * -50}deg) scale(${speed},${speed})`;
      });
    });
  },
};
</script>

<style lang="less">
body {
  background: radial-gradient(
    200% 100% at bottom center,
    #f7f7b6,
    #e96f92,
    #1b2947
  );
  background: radial-gradient(
    220% 105% at top center,
    #1b2947 10%,
    #75517d,
    #e96f92 65%,
    #f7f7b6
  );
  background-attachment: fixed;
}

// 动画
@keyframes rotate {
  0% {
    transform: perspective(400px) rotateZ(20deg) rotateX(-40deg) rotateY(0);
  }
  100% {
    transform: perspective(400px) rotateZ(20deg) rotateX(-40deg)
      rotateY(-360deg);
  }
}
.stars {
  transform: perspective(500px);
  transform-style: preserve-3d;
  position: absolute;
  perspective-origin: 50% 100%; // 透视圆点
  left: 50%;
  animation: rotate 90s infinite linear;
  bottom: 0;
}
.star {
  width: 2px;
  height: 2px;
  background: #f7f7b8;
  position: absolute;
  top: 0;
  left: 0;
  backface-visibility: hidden;
}
</style>
