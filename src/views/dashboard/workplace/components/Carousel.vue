<template>
  <a-carousel
    indicator-type="slider"
    show-arrow="hover"
    auto-play
    style="width: 100%; height: 150px; border-radius: 4px; overflow: hidden"
  >
    <a-carousel-item v-for="(image, idx) in images" :key="idx">
      <div>
        <a-link
          :href="image.url"
          target="_blank"
          rel="noopener"
        >
          <img :src="image.src" style="width: 100%" alt="" />
        </a-link>
      </div>
    </a-carousel-item>
  </a-carousel>
</template>

<script setup lang="ts">
const images = [
  {
    src: `http://124.221.255.18:9000/btlog/3306e9e3a31f4a69b30ed8e43168f317.JPG?${new Date().getTime()}`,
    url: 'http://shenbtw.online',
  },
  {
    src: `http://124.221.255.18:9000/btlog/3306e9e3a31f4a69b30ed8e43168f317.JPG?${new Date().getTime()}`,
    url: 'http://shenbtw.online',
  },
]
</script>
