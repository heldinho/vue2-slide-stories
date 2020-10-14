<template>
  <div :data-slide="`slide-${slideId}`" class="slide">
    <div class="slide-items">
      <img
        v-for="(img, index) in images"
        :src="img.src"
        :alt="img.alt"
        :key="index"
      />
    </div>
    <nav class="slide-nav">
      <div class="slide-thumb">
        <span v-for="(span, index) in images" :key="index"></span>
      </div>
      <button class="slide-prev" @click="prev()">Anterior</button>
      <button class="slide-next" @click="next()">Próximo</button>
    </nav>
  </div>
</template>

<script>
export default {
  props: ['slideId', 'images'],
  data: () => ({
    active: 0,
    thumb: null,
    thumbItems: null,
    slide: null,
    items: null
  }),
  mounted() {
    this.slide = document.querySelector(`[data-slide="slide-${this.slideId}"]`)
    this.init()
  },
  methods: {
    activeSlide: function(index) {
      this.active = index
      this.items.forEach(item => item.classList.remove('active'))
      this.items[index].classList.add('active') // imagens da DOM - add active in items[index]
      this.thumbItems.forEach(item => item.classList.remove('active'))
      this.thumbItems[index].classList.add('active')
      this.autoSlide()
    },

    prev: function() {
      if (this.active > 0) {
        this.activeSlide(this.active - 1)
      } else {
        this.activeSlide(this.items.length - 1)
      }
    },

    next: function() {
      if (this.active < this.items.length - 1) {
        this.activeSlide(this.active + 1)
      } else {
        this.activeSlide(0)
      }
    },

    addThumbItems: function() {
      this.thumbItems = Array.from(this.thumb.children)
    },

    autoSlide() {
      clearTimeout(this.timeout)
      this.timeout = setTimeout(this.next, 5100)
    },

    init: function() {
      this.items = this.slide.querySelectorAll('.slide-items > *')
      this.thumb = this.slide.querySelector('.slide-thumb')
      this.addThumbItems()
      this.activeSlide(0)
    }
  }
}
</script>

<style lang="scss">
body {
  background: #1b1d20;

  img {
    max-width: 100%;
    display: block;
  }

  .slide {
    max-width: 380px;
    margin: 20px auto;
    display: grid;
    box-shadow: 0 4px 20px 2px rgba(0, 0, 0, 0.4);

    .slide-items {
      position: relative;
      grid-area: 1/1;
      border-radius: 5px;
      overflow: hidden;

      & > * {
        position: absolute;
        top: 0px;
        opacity: 0;
        pointer-events: none;
      }

      & > .active {
        position: relative;
        opacity: 1;
        pointer-events: initial;
      }
    }
    .slide-nav {
      position: relative;
      grid-area: 1/1;
      z-index: 1;
      display: grid;
      grid-template-columns: 1fr 1fr;
      grid-template-rows: auto 1fr;

      .slide-thumb {
        display: flex;
        grid-column: 1 / 3;

        & > span {
          flex: 1;
          display: block;
          height: 3px;
          background: rgba(0, 0, 0, 0.4);
          margin: 5px;
          border-radius: 3px;
          overflow: hidden;
        }

        & > span.active::after {
          content: '';
          display: block;
          height: inherit;
          background: rgba(255, 255, 255, 0.9);
          border-radius: 3px;
          transform: translateX(-100%);
          animation: thumb 5s forwards linear;
        }
      }

      button {
        width: 100px;
        -webkit-appearance: none;
        -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
        opacity: 0;

        &.slide-prev {
          position: absolute;
          left: 0;
          top: 12px;
          height: calc(100% - 12px);
        }
        &.slide-next {
          position: absolute;
          right: 0;
          top: 12px;
          height: calc(100% - 12px);
        }
      }
    }
  }
}

@keyframes thumb {
  to {
    transform: initial;
  }
}
</style>
