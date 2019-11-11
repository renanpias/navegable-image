<template>
  <div class="navegable-image">
    <div class="img-wrapper" :style="`background-image: url('${this.img}')`">
        <img :src="this.img" :alt="this.alt" class="image normal-zoom">
    </div>
  </div>
</template>

<script>
export default {
  name: 'NavegableImage',
  props: {
    img: {
      type: String,
      required: true
    },
    imagezoom: {
      type: String,
      default: '1.8'
    },
    alt: {
      type: String
    }
  },
  mounted() {
    this.zoom()
  },
  methods: {
    zoom() {
      const elemImg = document.querySelector('.image')
      elemImg.addEventListener('mousemove', (event) => {
        const bbox = event.target.getBoundingClientRect()
        const mouseX = event.clientX - bbox.left
        const mouseY = event.clientY - bbox.top
        const xPercent = (mouseX / bbox.width) * 100
        const yPercent = (mouseY / bbox.height) * 100
        elemImg.style.transformOrigin = (xPercent + '%' + yPercent + '%') // eslint-disable-line
      })
      elemImg.addEventListener('mouseenter', () => {
        elemImg.classList.add('zoom-in')
        elemImg.classList.remove('normal-zoom')
        elemImg.style.transform = `scale(${this.imagezoom})`
      })
      elemImg.addEventListener('mouseleave', () => {
        elemImg.classList.add('normal-zoom')
        elemImg.classList.remove('zoom-in')
      })
    }
  }
}
</script>
<style lang="scss" scoped>
.navegable-image {
  .img-wrapper {
    background-size: 100%;
    .image {
        width: 100%;
        height: 100%;
    }
    .normal-zoom {
        opacity: 0;
        transform: scale(1);
        cursor: zoom-in;
        transition: opacity 300ms;
    }
    .zoom-in {
        opacity: 1;
        cursor: zoom-in;
        transition: opacity 300ms;
    }
  }
}
</style>
