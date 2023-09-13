<template>
  <div class="pt-28 lg:pt-36 h-screen bg-green-500 flex flex-col justify-start items-center">
    <h1 class="text-white text-4xl lg:text-5xl">Works</h1>
    <Slider :imageBefore="beforeImage" :imageAfter="afterImage" />
  </div>
</template>

<script>
import Slider from './Slider.vue';

// Importujte obrázky přímo
import beforeImage from 'srcDir/components/before-image.jpg';
import afterImage from 'srcDir/components/after-image.jpg';

export default {
  components: {
    Slider
  },
  data() {
    return {
      beforeImage,
      afterImage
    }
  }
}
</script>

