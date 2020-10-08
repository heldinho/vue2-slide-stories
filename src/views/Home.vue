<template>
  <div class="home">
    <SlideStories :items="items" />
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
    items: mapImages
  })
}
</script>
