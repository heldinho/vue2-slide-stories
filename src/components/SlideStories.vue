<template>
  <div data-slide="slide" class="slide">
    <div class="slide-items">
      <img v-for="{ src, alt, id } in items" :src="src" :alt="alt" :key="id" />
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
  props: {
    items: [Array, Object]
  },
  data: () => ({
    active: 0,
    thumb: null,
    slide: null
  }),
  mounted() {
    this.slide = document.querySelector(`[data-slide="slide"]`)
  },
  methods: {
    activeSlide: function (index) {
      this.active = index
      this.items.forEach(item => item.classList.remove('active'))
      this.item[index].classList.add('active')
      this.thumbItems.forEach(item => item.classList.remove('active'))
      this.thumbItems[index].classList.add('active')
    },

    prev: function () {
      if (this.active > 0) {
        this.activeSlide(this.active - 1)
      } else {
        this.activeSlide(this.items.length - 1)
      }
    },

    next: function () {
      if (this.active < this.items.length - 1) {
        this.activeSlide(this.active + 1)
      } else {
        this.activeSlide(0)
      }
    },

    addNavigation: function () {
      const nextBtn = this.slide.querySelector('.slide-next')
      const prevBtn = this.slide.querySelector('.slide-prev')
      nextBtn.addEventListener('click', this.next)
      prevBtn.addEventListener('click', this.prev)
    },

    addThumbItems: function () {
      this.items.forEach(() => (this.thumb.innerHTML += `<span></span>`))
      this.thumbItems = Array.from(this.thumb.children)
    },

    init: function () {
      this.next = this.next.bind(this)
      this.prev = this.prev.bind(this)
      this.items = this.slide.querySelectorAll('.slide-items > *')
      this.thumb = this.slide.querySelector('.slide-thumb')
      this.addThumbItems()
      this.activeSlide(0)
      this.addNavigation()
    }

  }
}
</script>

<style lang="scss" scoped>
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
        -webkit-appearance: none;
        -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
        opacity: 0;
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
