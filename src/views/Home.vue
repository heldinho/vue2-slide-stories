<template>
  <div class="home">
    <SlideStories slideId="girafa" :images="images" />
    <SlideStories slideId="background" :images="background" />
  </div>
</template>

<script>
// @ is an alias to /src
import SlideStories from '@/components/SlideStories'
import mapImages from '@/components/mapImages'
import mapImgBackground from '@/components/mapImgBackground'

export default {
  components: {
    SlideStories
  },
  data: () => ({
    images: mapImages,
    background: mapImgBackground
  })
}
</script>
