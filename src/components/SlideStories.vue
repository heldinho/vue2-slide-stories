<template>
  <div data-slide="slide" class="slide">
    <div class="slide-items">
      <img v-for="{ src, alt, id } in images" :src="src" :alt="alt" :key="id" />
    </div>
    <nav class="slide-nav">
      <div class="slide-thumb"></div>
      <button class="slide-prev">Anterior</button>
      <button class="slide-next">Próximo</button>
    </nav>
  </div>
</template>

<script>
export default {
  name: 'SlideStories',
  data: () => ({
    active: 0
  }),
  methods: {}
}
</script>

<style lang="scss" scoped>
</style>
