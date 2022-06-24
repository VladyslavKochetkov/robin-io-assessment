<script setup lang="ts">
import { reactive, onMounted } from "vue";

const getSpeed = () => Math.round(Math.random() * 180);

const state = reactive({ speed: 0, animation: true });

function toggleAnimations() {
  state.animation = !state.animation;
}

onMounted(() => {
  setTimeout(() => (state.speed = getSpeed()), 50);
  setInterval(() => {
    state.speed = getSpeed();
  }, 4000);
});
</script>

<template>
  <div class="speedometer-container">
    <div class="speedometer">
      <img
        class="dial"
        src="@/assets/images/dial.png"
        :style="{
          transform: `translate(-50%, -90%) rotate(${
            -122 + (244 / 180) * state.speed
          }deg)`,
          transitionDuration: `${state.animation ? '3600ms' : '0ms'}`,
        }"
      />
      <img
        class="speedometer-bg"
        src="@/assets/images/meter.png"
        :style="{
          backgroundColor: `${
            state.speed <= 60
              ? 'rgba(0, 255, 0, 0.2)'
              : state.speed <= 120
              ? 'rgba(255, 165, 0, 0.2)'
              : 'rgba(255, 0, 0, 0.2)'
          }`,
          transitionDuration: `${state.animation ? '3600ms' : '0ms'}`,
        }"
      />
    </div>
    <span>Speed: {{ state.speed }}</span>
    <button @click="toggleAnimations">
      Toggle Animations (Currently: {{ state.animation ? "On" : "Off" }})
    </button>
  </div>
</template>

<style scoped>
.speedometer-container {
  display: flex;
  flex-direction: column;
  gap: 15px;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
}
.speedometer {
  position: relative;
}
.speedometer-bg {
  transition: background-color ease-out 3600ms;
}
.dial {
  position: absolute;
  top: 50%;
  left: 50%;
  transform-origin: center 85%;
  transition: transform ease-out 3600ms;
}
</style>
