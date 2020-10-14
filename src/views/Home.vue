<template>
  <div class="home">
    <SlideStories slideId="girafa" :images="images" />
  </div>
</template>

<script>
// @ is an alias to /src
import SlideStories from '@/components/SlideStories'
import mapImages from '@/components/mapImages'

export default {
  components: {
    SlideStories
  },
  data: () => ({
    images: mapImages
  })
}
</script>
