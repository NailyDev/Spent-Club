<script setup>
import slide1 from '@/assets/image 47.png'
import slide2 from '@/assets/image 46.png'
import slide3 from '@/assets/image 49.png'
import slide4 from '@/assets/image 50.png'
import slide5 from '@/assets/image 52.png'
import slide6 from '@/assets/imageSlide.png'
import AboutInformation from './components/AboutInformation.vue'
import Header from './components/Header.vue'
import HomeLogo from './components/HomeLogo.vue'
import ImageSlider from './components/ImageSlider.vue'
</script>

<template>
  <Header/>
  <HomeLogo/>
  <AboutInformation/>
  <div class="max-w-4xl mx-auto px-4 py-12">
    <ImageSlider :images="[slide1, slide2, slide3, slide4, slide5, slide6]" />
  </div>
</template>