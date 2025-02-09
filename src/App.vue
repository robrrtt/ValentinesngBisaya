<template>
<div :class="['relative', 'flex', 'items-center', 'justify-center', 'h-screen', { 'bg-pink-200': !accepted, 'bg-green-200': accepted }]">    <!-- Floating Hearts and Roses Animation -->
    <div v-for="(heart, index) in hearts" :key="index" class="absolute">
      <span
        class="text-red-500 text-5xl absolute animate-float"
        :style="{
          top: heart.y + 'px',
          left: heart.x + 'px',
          animationDelay: heart.delay + 's',
        }"
      >❤️</span>
    </div>

    <div v-for="(rose, index) in roses" :key="'rose' + index" class="absolute">
      <span
        class="text-red-600 text-5xl absolute animate-float"
        :style="{
          top: rose.y + 'px',
          left: rose.x + 'px',
          animationDelay: rose.delay + 's',
        }"
      >🌹</span>
    </div>

    <!-- Card -->
    <div class="text-center bg-white p-10 rounded-2xl shadow-xl max-w-md relative">
      <h1 class="text-3xl font-bold text-pink-600">Will you be my Valentine? ❤️</h1>
      <div class="flex justify-center gap-4 mt-4">
        <button 
  @click="sayYes"
  aria-label="Accept the Valentine's Day invitation"
  class="bg-pink-500 text-white px-6 py-2 rounded-lg hover:bg-pink-700 transition">
  Yes 💖
</button>
        <button 
          @mouseover="moveNo"
          ref="noButton"
          class="bg-gray-400 text-white px-6 py-2 rounded-lg cursor-pointer absolute">
          No 😢
        </button>
      </div>
      <p v-if="accepted" class="mt-4 text-xl text-green-600 font-semibold">Yay! Can't wait for our date! 🎉</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      accepted: false,
      hearts: [],
      roses: [],
    };
  },
  mounted() {
    this.createFloatingEmojis();
  },
  methods: {
    sayYes() {
      this.accepted = true;
    },
    moveNo() {
  const btn = this.$refs.noButton;
  const rect = btn.getBoundingClientRect();
  const maxX = window.innerWidth - rect.width;
  const maxY = window.innerHeight - rect.height;

  // Move the button to a random position within the viewport
  btn.style.top = `${Math.random() * maxY}px`;
  btn.style.left = `${Math.random() * maxX}px`;

  // Optional: Add a slight rotation for fun
  btn.style.transform = `rotate(${Math.random() * 360}deg)`;
},
    createFloatingEmojis() {
      for (let i = 0; i < 15; i++) {
        this.hearts.push({
          x: Math.random() * window.innerWidth,
          y: Math.random() * window.innerHeight,
          delay: Math.random() * 5,
        });
        this.roses.push({
          x: Math.random() * window.innerWidth,
          y: Math.random() * window.innerHeight,
          delay: Math.random() * 5,
        });
      }
    },
  },
};
</script>

<style>
@keyframes floatUp {
  0% {
    transform: translateY(100vh) rotate(0deg);
    opacity: 0;
  }
  50% {
    opacity: 1;
  }
  100% {
    transform: translateY(-10vh) rotate(360deg);
    opacity: 0;
  }
}

.animate-float {
  animation: floatUp 5s linear infinite;
  position: absolute;
}
</style>
