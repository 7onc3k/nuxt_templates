<template>
    <div class="before-after-container" ref="container">
      <img :src="imageBefore" class="image-before">
      <div class="slider" ref="slider">
        <img :src="imageAfter" class="image-after">
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      imageBefore: String,
      imageAfter: String
    },
    mounted() {
      this.sliderWidth = this.$refs.slider.offsetWidth;
      this.containerWidth = this.$refs.container.offsetWidth;
  
      this.$refs.container.addEventListener('mousemove', this.handleMouseMove);
      this.$refs.container.addEventListener('touchmove', this.handleMouseMove);
    },
    beforeDestroy() {
      this.$refs.container.removeEventListener('mousemove', this.handleMouseMove);
      this.$refs.container.removeEventListener('touchmove', this.handleMouseMove);
    },
    methods: {
      handleMouseMove(event) {
        const x = event.pageX - this.$refs.container.offsetLeft;
        const width = Math.min(this.containerWidth, Math.max(0, x));
        this.$refs.slider.style.width = `${width}px`;
      }
    }
  }
  </script>
  
  <style scoped>
  .before-after-container {
    position: relative;
    width: 100%;
    overflow: hidden;
  }
  
  .image-before, .image-after {
    width: 100%;
    display: block;
  }
  
  .slider {
    position: absolute;
    top: 0;
    left: 0;
    width: 50%;
    overflow: hidden;
  }
  </style>
  