<template>
  <div
    class="home-container relative w-screen h-screen bg-white overflow-hidden"
  >
    <div
      class="
        loading
        w-full
        h-full
        flex
        justify-center
        items-center
        z-30
        absolute
      "
    >
      <h1 id="demo">0%</h1>
    </div>
    <Menu class="cmpt-menu absolute top-0 z-20"></Menu>
    <Navbar class="cmpt-navbar absolute top-0 z-10"></Navbar>
    <div class="home-content absolute top-0 flex" ref="homeContent">
      <ul class="flex" ref="scoller">
        <li class="card-box c1"><Card></Card></li>
        <li class="card-box c2"><Card></Card></li>
        <li class="card-box c3"><Card></Card></li>
        <li class="card-box c4"><Card></Card></li>
        <li class="card-box c5"><Card></Card></li>
        <li class="card-box c6"><Card></Card></li>
        <li class="card-box c7"><Card></Card></li>
        <li class="card-box c8"><Card></Card></li>
      </ul>
      <!-- <span class="home-content-bg">latest</span> -->
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import anime from "animejs/lib/anime.es.js";
import gsap from "gsap";

import Menu from "../components/Menu.vue";
import Navbar from "../components/Navbar.vue";
import Card from "../components/Card.vue";

defineProps({
  msg: String,
});

// 菜单父级
const homeContent = ref(null);
// 菜单所有菜单

onMounted(() => {
  const tl = anime.timeline({
    easing: "easeOutExpo",
    duration: 750,
  });
  tl.add({
    targets: "#demo",
    innerHTML: ["0%", "100%"],
    round: 1,
    easing: "easeInOutExpo",
    duration: 4000,
  });
  tl.add(
    {
      targets: "#demo",
      rotateY: -20,
      rotateX: -20,
      rotateZ: 0,
      color: "#a72c32",
    },
    "-=800"
  );
  tl.add(
    {
      targets: "#demo",
      rotateY: 120,
      rotateX: 120,
      rotateZ: 0,
      scale: 0,
      easing: "easeInOutExpo",
    },
    "-=200"
  );
  tl.add(
    {
      targets: "#demo",
      opacity: 0,
      easing: "easeInOutExpo",
    },
    "-=400"
  );
  tl.add({
    targets: ".loading",
    opacity: 0,
    complete: () => {
      document.querySelector(".loading").style.display = "none";
    },
  });
  tl.add(
    {
      targets: ".cmpt-menu",
      translateX: [-96, 0],
      easing: "easeInOutExpo",
      duration: 500,
    },
    "-=800"
  );
  tl.add(
    {
      targets: ".cmpt-navbar",
      translateY: [-80, 0],
      easing: "easeInOutExpo",
      duration: 500,
    },
    "-=800"
  );
  tl.add(
    {
      targets: ".home-content",
      opacity: [0, 1],
      easing: "easeInOutExpo",
      duration: 500,
    },
    "-=800"
  );

  const homeContent = document.querySelector(".home-content");

  const cardBoxs = document.querySelectorAll(".card-box");

  let scrollSpeed = 0;
  let oldScrollX = 0;
  let scrollX = 0;
  let x = 0;

  // mousewheel
  // 滚动坐标 -= 鼠标滚轮坐标
  const handleMouseWheel = (e) => {
    let deltaX = e.deltaX;

    if (deltaX > 25) {
      deltaX = 25;
    }
    if (deltaX < -25) {
      deltaX = -25;
    }
    scrollX -= deltaX;
  };

  const lerp = (v0, v1, t) => {
    return v0 * (1 - t) + v1 * t;
  };

  // 滚动事件
  homeContent.addEventListener("mousewheel", handleMouseWheel);

  const render = () => {
    requestAnimationFrame(render);
    x = lerp(x, scrollX, 0.1);

    scrollSpeed = x - oldScrollX;
    oldScrollX = x;

    // 方向
    let direction = scrollSpeed > 0 ? 1 : -1;

    gsap.to(cardBoxs, {
      scale: 1 - Math.min(100, Math.abs(scrollSpeed)) * 0.005,
      // rotate: scrollSpeed * 0.2,
      rotateX: scrollSpeed * 1.2,
      rotateY: scrollSpeed * 1.2 * direction,
      duration: 0.01,
    });
  };
  render();
});
</script>

<style scoped>
#demo {
  font-family: "Russo One", sans-serif;
}
.loading {
  transform-style: preserve-3d;
  perspective: 400px;
}
.loading > h1 {
  font-size: 10rem;
}

.home-content {
  /* z-index: -1; */
  position: absolute;
  left: 96px;
  top: 80px;
  right: 0;
  bottom: 0;
  overflow: auto;
  /* background: #000; */
}

.home-content-bg {
  font-size: 20rem;
  font-weight: 900;
  text-transform: uppercase;
  position: absolute;
  top: 50%;
  left: 55%;
  color: #f6f5ef;
  transform: translate(-50%, -50%);
  z-index: 0;
}

.card-box {
  /* position: absolute; */
  z-index: 1;
  /* top: 0;
  left: 0; */
  width: 400px;
  height: 100%;
  display: grid;
  align-items: end;
  transition: all 0.2s;
  padding-bottom: 100px;
  /* transform: rotateY(25deg) rotateX(-25deg); */
}
.card-box:nth-child(odd) > #Card {
  align-self: start;
  padding-bottom: 0px;
}
</style>
