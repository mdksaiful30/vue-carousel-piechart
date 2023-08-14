<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';
const images = [
  'https://images.unsplash.com/photo-1494438639946-1ebd1d20bf85?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1467&q=80',
  'https://images.unsplash.com/photo-1505691938895-1758d7feb511?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80',
  'https://images.unsplash.com/photo-1558882224-dda166733046?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1469&q=80',
  'https://images.unsplash.com/photo-1562664377-709f2c337eb2?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80',
  'https://images.unsplash.com/photo-1476514525535-07fb3b4ae5f1?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80',
  'https://images.unsplash.com/photo-1507525428034-b723cf961d3e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1473&q=80',
];
const currentIndex = ref(0);
const currentImage = ref(images[currentIndex.value]);
const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % images.length;
  currentImage.value = images[currentIndex.value];
};
const prevSlide = () => {
  currentIndex.value = (currentIndex.value - 1 + images.length) % images.length;
  currentImage.value = images[currentIndex.value];
};
const interval = setInterval(nextSlide, 2000); // Auto advance every 2 seconds

onMounted(() => {
  console.log('Carousel initialized');
});

onBeforeUnmount(() => {
  clearInterval(interval); // Clear the interval to prevent memory leaks
  console.log('Carousel cleanup');
});

</script>
<template>
  <div class="carousel">
    <div class="slide" :style="{ backgroundImage: `url(${currentImage})` }"></div>
    <button @click="prevSlide">Previous</button>
    <button @click="nextSlide">Next</button>
  </div>
</template>

<style scoped>
.carousel {
  position: relative;
  width: 100%;
  height: 600px;
  overflow: hidden;
}
.slide {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 800px;
  background-size: cover;
  background-position: center;
}
button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 100px;
  height: 50px;
  background-color: lightseagreen;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
button:hover {
  background-color: #ddd;
}
button:active {
  background-color: #bbb;
}
button:first-child {
  left: 0;
}
button:last-child {
  right: 0;
}

</style>