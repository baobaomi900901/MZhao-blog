<!--
* @description  参数1
* @fileName  Card
* @author userName
* @date 2022-05-03 19:35:35
* @version V3.0.0
!-->
<template>
  <!-- style="matrix(0,1,-1,0,0,0)" -->
  <div id="Card" class="Card">
    <p class="card-tag" ref="cardTag">Music Video</p>
    <img src="../assets/demo.jpeg" alt="" class="card-img" ref="cardImg" />
    <div class="card-img-bg" ref="cardImgBg">
      <p class="card-title absolute">DEMDIKE STARE- SYMBIOSIS</p>
    </div>
    <div class="card-tag-subtag" ref="cardTagSubtag">
      <p>electronic</p>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import anime from "animejs/lib/anime.es.js";
export default {
  name: "Card",
  setup() {
    const Card = ref(null);
    const cardImg = ref(null);
    const cardImgBg = ref(null);
    const cardTag = ref(null);
    const cardTagSubtag = ref(null);
    // 偏移角度
    const mostX = 10; // 10 or -10
    const mostY = 10; // 10 or -10
    onMounted(() => {
      let rotationY = 0;
      let rotationX = 0;
      cardImg.value.style.transform = `translate(-50%, -50%)`;
      cardImg.value.style.top = `45%`;
      cardImg.value.style.left = `45%`;

      cardImgBg.value.style.transform = `translate(-50%, -50%)`;
      cardImgBg.value.style.top = `50%`;
      cardImgBg.value.style.left = `50%`;

      cardTag.value.style.transform = `translate(-50%, -50%)`;
      cardTag.value.style.top = `10%`;
      cardTag.value.style.left = `26%`;

      cardTagSubtag.value.style.transform = `rotateZ(-90deg)`;
      cardTagSubtag.value.style.top = `13%`;
      cardTagSubtag.value.style.left = `-22%`;

      cardImg.value.addEventListener("mousemove", (event) => {
        cardImg.value.style.transition = "none";
        cardImgBg.value.style.transition = "none";
        cardTag.value.style.transition = "none";
        cardTagSubtag.value.style.transition = "none";

        const x = event.offsetX;
        const y = event.offsetY;
        // el.getBoundingClientRect() 返回元素的位置和大小
        const { width, height } = cardImg.value.getBoundingClientRect();
        const halfWidth = width / 2;
        const halfHeight = height / 2;

        // 计算角度, 这里的 y 是相反的
        rotationY = ((x - halfWidth) / halfWidth) * mostX;
        rotationX = ((y - halfHeight) / halfHeight) * mostY * -1;
        const rotationZ = ((y - halfWidth) / halfWidth) * 10;
        const rotationZ2 = ((y - halfWidth) / halfWidth) * 5;

        const translateY = ((y - halfWidth) / halfWidth) * -20;
        const translateX = ((y - x) / halfHeight) * -20;
        let rotationVar = y / halfWidth;
        rotationVar = rotationVar > 1 ? rotationVar : rotationVar + 1;

        // 设置偏移
        cardImg.value.style.transform = `translate(-50%, -50%) rotateY(${rotationY}deg) rotateX(${rotationX}deg)`;

        // card-img-bg
        cardImgBg.value.style.transform = `translate(-50%, -50%) rotateY(${
          rotationY / rotationVar
        }deg) rotateX(${
          rotationX / rotationVar
        }deg) translateX(${translateX}px) translateY(${translateY}px)`;

        cardTag.value.style.transform = `translate(-50%, -50%) rotateY(${
          rotationY - 5
        }deg) rotateX(${
          rotationX - 5
        }deg) rotateZ(${rotationZ}deg) translateX(${translateX}px) translateY(${translateY}px)`;

        cardTagSubtag.value.style.transform = `rotateY(${
          rotationY - 5
        }deg) rotateX(${rotationX - 5}deg) rotateZ(${
          rotationZ2 - 90
        }deg) translateX(${translateX - 10}px) `;
      });

      cardImg.value.addEventListener("mouseout", (event) => {
        cardImg.value.style.transition =
          "transform 0.5s cubic-bezier(.27,-0.85,.54,2.01)";
        cardImg.value.style.transform = `translate(-50%, -50%) rotateY(0) rotateX(0)`;

        cardImgBg.value.style.transition = "transform 0.5s ease-in-out";
        cardImgBg.value.style.transform = `translate(-50%, -50%)  rotateY(0) rotateX(0)`;

        cardTag.value.style.transition = "transform 0.5s ease-in-out";
        cardTag.value.style.transform = `translate(-50%, -50%) rotateY(0) rotateX(0) rotateZ(0) translateX(0px) translateY(0px)`;

        cardTagSubtag.value.style.transition = "transform 0.5s ease-in-out";
        cardTagSubtag.value.style.transform = `rotateY(0) rotateX(0) rotateZ(-90deg) `;
      });
    });
    return { cardImg, Card, cardImgBg, cardTag, cardTagSubtag };
  },
};
</script>
<style scoped>
.Card {
  justify-content: center;
  padding: 80px 0px;
  position: relative;
  perspective: 1000px;
  width: 480px;
  height: 480px;
}
.card-img {
  width: 300px;
  height: 300px;
  position: absolute;
  z-index: 1;
  transition: border 0.5s;
  transform: translateX(100px) translateY(100px);
}

.card-tag {
  position: absolute;
  font-size: 0.875rem;
  font-weight: 900;
}

.card-img:hover ~ .card-img-bg {
  border: 5px solid #000;
}

.card-img-bg {
  content: "";
  position: absolute;
  width: 300px;
  height: 300px;
  border: 4px solid #000;
  z-index: 0;
  transition: border 0.5s;
}
.card-tag-subtag {
  position: absolute;
  transform-origin: right;
  max-width: 150px;
  width: 100%;
  text-align: end;
  font-weight: 500;
  font-size: 0.875rem;
}
.card-title {
  width: 80%;
  bottom: -70px;
  right: -25px;
  font-size: 1.25rem;
  font-weight: 900;
  text-align: end;
}
</style>