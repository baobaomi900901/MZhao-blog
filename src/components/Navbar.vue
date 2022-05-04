<!--
* @description  参数1
* @fileName  Navbar
* @author userName
* @date 2022-05-03 18:23:01
* @version V3.0.0
!-->
<template>
  <div id="Navbar" class="navbar border-b flex justify-end items-center border-gray-300">
    <img src="../assets/MansteinZhao.png" alt="" class="web-title absolute" />
    <div class="navbar-links flex gap-10 mr-10 font-bold">
      <div class="navbar-link cursor-pointer">FACEBOOK</div>
      <div class="navbar-link cursor-pointer">TWITTER</div>
      <div class="navbar-link cursor-pointer">INSTAGRAM</div>
      <div class="navbar-link cursor-pointer">CODEPEN</div>
      <div class="navbar-link cursor-pointer">GITHUB</div>
    </div>
  </div>
</template>

<script>
import { ref, reactive } from "vue";
export default {
  name: "Navbar",
  setup() {
    return {};
  },
};
</script>
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Russo+One&family=Titillium+Web:ital,wght@0,200;0,300;0,400;0,600;0,700;0,900;1,200;1,300;1,400;1,600;1,700&display=swap");
#Navbar {
  width: 100%;
  height: 5rem;
  background: #fff;
  font-family: "Titillium Web", sans-serif;
}
.navbar > .web-title {
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(0.75);
}

.navbar-link {
  transition:  opacity 0.5s cubic-bezier(0.77, 0.2, 0.05, 1);
}

.navbar-link:hover {
  opacity: 0.55;
}

</style>