<template>
  <div id="app">
    <!-- Header -->
    <header class="header">
      <h1>Rama Vue App</h1>
    </header>

    <!-- Click Counter -->
    <section class="section counter">
      <h2>Click Counter</h2>
      <div class="counter-box">
        <p class="count-display">{{ count }}</p>
        <button @click="incrementCount" class="btn primary">Click Me!</button>
      </div>
    </section>

    <!-- Box Color Changer -->
    <section class="section color-changer">
      <h2>Box Color Changer</h2>
      <div :style="{ backgroundColor: currentColor }" class="color-box"></div>
      <button @click="changeColor" class="btn secondary">Change Color</button>
    </section>

    <!-- Image Carousel -->
    <section class="section carousel">
      <h2>Image Carousel</h2>
      <div class="carousel-container">
        <transition name="fade" mode="out-in">
          <img :src="images[currentImage]" :key="images[currentImage]" alt="carousel image" class="carousel-image" />
        </transition>
      </div>
      <div class="carousel-controls">
        <button @click="prevImage" class="btn prev">Previous</button>
        <button @click="nextImage" class="btn next">Next</button>
      </div>
    </section>
  </div>
</template>

<script>
import { ref, computed } from "vue";

export default {
  setup() {
    // Click Counter
    const count = ref(0);
    const incrementCount = () => {
      count.value++;
    };

    // Box Color Changer
    const colors = ['#ff7f50', '#6495ed', '#3cb371', '#ffd700', '#ee82ee'];
    const currentColorIndex = ref(0);
    const currentColor = computed(() => colors[currentColorIndex.value]);
    const changeColor = () => {
      currentColorIndex.value = (currentColorIndex.value + 1) % colors.length;
    };

    // Image Carousel
    const images = [
      'https://cdn.pixabay.com/photo/2024/09/01/14/02/spider-9014068_1280.jpg',
      'https://cdn.pixabay.com/photo/2024/09/05/12/55/white-cheeked-turaco-9024880_1280.jpg',
      'https://cdn.pixabay.com/photo/2023/09/03/12/16/lizard-8230594_1280.png'
    ];
    const currentImage = ref(0);
    const prevImage = () => {
      currentImage.value = (currentImage.value + images.length - 1) % images.length;
    };
    const nextImage = () => {
      currentImage.value = (currentImage.value + 1) % images.length;
    };

    return {
      count, incrementCount,
      currentColor, changeColor,
      images, currentImage, prevImage, nextImage
    };
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');

* {
  box-sizing: border-box;
}

body {
  font-family: 'Poppins', sans-serif;
  margin: 0;
  padding: 0;
}

#app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
}

.header h1 {
  font-size: 2.5rem;
  margin-bottom: 20px;
  color: #333;
}

.section {
  margin: 30px 0;
}

.counter-box {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.count-display {
  font-size: 3rem;
  margin-bottom: 15px;
  color: #555;
}

.color-box {
  width: 150px;
  height: 150px;
  margin: 20px auto;
  transition: background-color 0.5s ease;
  border-radius: 12px;
}

.carousel-container {
  width: 500px;
  height: 400px;
  margin: 25px auto;
  overflow: hidden;
  position: relative;
}

.carousel-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 10px;
}

.carousel-controls {
  display: flex;
  justify-content: center;
  gap: 15px;
  margin-top: 10px;
}

.btn {
  padding: 10px 20px;
  font-size: 1rem;
  cursor: pointer;
  border: none;
  border-radius: 5px;
  transition: background-color 0.3s ease;
}

.primary {
  background-color: #3498db;
  color: white;
}

.primary:hover {
  background-color: #2980b9;
}

.secondary {
  background-color: #2ecc71;
  color: white;
}

.secondary:hover {
  background-color: #27ae60;
}

.prev {
  background-color: #e74c3c;
  color: white;
}

.prev:hover {
  background-color: #c0392b;
}

.next {
  background-color: #9b59b6;
  color: white;
}

.next:hover {
  background-color: #8e44ad;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
