<!--
* @description  参数1
* @fileName  Menu
* @author userName
* @date 2022-05-03 09:41:42
* @version V3.0.0
!-->
<template>
  <div
    id="Menu"
    class="
      menu
      w-24
      h-screen
      bg-white
      border-r border-gray-300
      flex flex-col
      items-center
    "
  >
    <div class="menu-hamburger-icon flex flex-col mt-10">
      <input type="checkbox" />
      <span></span>
      <span></span>
      <span></span>
    </div>

    <ul class="menu-items mt-4">
      <li class="menu-item cursor-pointer">new photo</li>
      <li class="menu-item cursor-pointer">on repeat</li>
      <li class="menu-item cursor-pointer">music videos</li>
      <li class="menu-item cursor-pointer">crosstalk</li>
    </ul>
  </div>
</template>

<script>
import { ref, reactive } from "vue";
export default {
  name: "Menu",
  setup() {
    return {};
  },
};
</script>
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Russo+One&family=Titillium+Web:ital,wght@0,200;0,300;0,400;0,600;0,700;0,900;1,200;1,300;1,400;1,600;1,700&display=swap");
#Menu {
  /* font-family: "Russo One", sans-serif; */
  font-family: "Titillium Web", sans-serif;
}
.menu-hamburger-icon > input {
  display: block;
  width: 40px;
  height: 40px;
  position: absolute;
  top: 32px;
  left: 50%;
  transform: translate(-50%, 0);

  cursor: pointer;
  border: 1px solid #ccc;

  opacity: 0;
  z-index: 2; /* and place it over the hamburger */

  -webkit-touch-callout: none;
}

.menu-hamburger-icon > span {
  display: inline-block;
  width: 34px;
  height: 4px;
  background: #000;

  border-radius: 3px;
  margin-bottom: 6px;
  z-index: 1;

  transform-origin: 4px 0px;

  transition: transform 0.5s cubic-bezier(0.77, 0.2, 0.05, 1),
    background 0.5s cubic-bezier(0.77, 0.2, 0.05, 1), opacity 0.55s ease;
}

.menu-hamburger-icon > span:first-child {
  transform-origin: 0% 50%;
}
.menu-hamburger-icon > span:nth-last-child(2) {
  transform-origin: 50% 50%;
}
.menu-hamburger-icon > span:nth-last-child(3) {
  transform-origin: 0% 50%;
}

.menu-hamburger-icon > input:checked ~ span {
  opacity: 1;
  transform: rotate(45deg) translate(-2px, -2px);
  background: #fff;
}
.menu-hamburger-icon > input:checked ~ span:nth-last-child(2) {
  opacity: 1;
  transform: rotate(0deg) scale(0, 0) translate(-2px, -1px);
}

.menu-hamburger-icon > input:checked ~ span:nth-last-child(1) {
  transform: rotate(-45deg) translate(0, -2px);
}

.menu-items {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  /* background: #ccc; */
  text-overflow: clip;
  overflow-wrap: normal;
}
.menu-item {
  position: relative;
  text-transform: uppercase;
  display: inline-block;
  white-space: normal;
  overflow: hidden;
  transition:  color 0.2s ease;
}

.menu-item::before {
  content: "";
  background: #a72c32;
  position: absolute;
  transform: translate(0%, -50%);
  top: 50%;
  width: 100%;
  height: 1px;
  animation: meunItemAnimationOut 0.5s forwards;
}

.menu-item:hover {
  color: #999;
}

.menu-item:hover::before {
  background: #a72c32;
  animation: meunItemAnimationIn 0.5s forwards;
}

@keyframes meunItemAnimationIn {
  0% {
    left: 100%;
  }
  100% {
    left: 0%;
  }
}

@keyframes meunItemAnimationOut {
  0% {
    left: 0%;
  }
  100% {
    left: -100%;
  }
}

.menu-items > .menu-item {
  /* background: rgba(255, 255, 255, 0.5); */
  /* background: red; */
  transform-origin: 50% 50%;
  /* transform: translate(-50%, 0); */
  transform: rotate(-90deg);
  /* width: 100px; */
  text-align: center;
  margin-top: 60px;
}

.menu-item:nth-child(3) {
  width: 112px;
}
.menu-items > .menu-item + .menu-item {
  margin-top: 120px;
}
</style>