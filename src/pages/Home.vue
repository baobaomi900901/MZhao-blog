<template>
  <div class="home-container relative w-screen h-screen bg-white">
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
    <div
      class="home-content w-full h-full absolute top-0 flex"
      ref="homeContent"
    >
      <div class="flex gap-10 overflow-scroll" ref="scoller">
        <div class="card-box"><Card></Card></div>
        <div class="card-box"><Card></Card></div>
        <div class="card-box"><Card></Card></div>
        <div class="card-box"><Card></Card></div>
        <div class="card-box"><Card></Card></div>
        <div class="card-box"><Card></Card></div>
      </div>
      <span class="home-content-bg">latest</span>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import anime from "animejs/lib/anime.es.js";

import Menu from "../components/Menu.vue";
import Navbar from "../components/Navbar.vue";
import Card from "../components/Card.vue";

defineProps({
  msg: String,
});

const count = ref(0);
const scoller = ref(null);
const homeContent = ref(null);
let barslast = 0;

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

  let last = 0;
  let on = false;

  scoller.value.addEventListener("mousewheel", (e) => {
    last = 1;
    document.querySelector(".card-box").style.transform = "none";
    scoller.value.scrollLeft -= e.deltaY;
    console.log(e.deltaY);
    if (e.deltaY > 0) {
      last = 1;
      anime({
        targets: ".card-box",
        rotateY: 25,
        rotateX: 25,
        duration: 100,
        complete: () => {
          last = 0;
          on = true;
        },
      });
    } else {
      last = -1;
      anime({
        targets: ".card-box",
        rotateY: 25,
        rotateX: -25,
        duration: 100,
        complete: () => {
          last = 0;
          on = true;
        },
      });
    }
  });

  setInterval(() => {
    if (last == 0 && on) {
      anime({
        targets: ".card-box",
        rotateY: 0,
        rotateX: 0,
        duration: 500,
        complete: () => {
          on = false;
        },
      });
    }
    // console.log(last);
  }, 100);
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
  padding-left: 96px;
  padding-top: 80px;
  overflow: hidden;
  height: 100%;
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
  z-index: 5;
  width: 400px;
  height: 100%;
  display: grid;
  align-items: end;
  /* transform: rotateY(25deg) rotateX(-25deg); */
}
.card-box:nth-child(odd) > #Card {
  align-self: start;
}
</style>
