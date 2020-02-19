<template>
  <div :class="sliderClass">
    <slot>
      <h4>this is the single slider</h4>
    </slot>
  </div>
</template>

<script>
import $ from 'jquery'
import slickMixin from 'slick-carousel'
import 'slick-carousel/slick/slick.css'
import 'slick-carousel/slick/slick-theme.css'

export default {
  name: 'Slider',
  mixins: [slickMixin],
  props: {
    sliderClass: {
      type: String,
      default: 'slider'
    },
    slides: {
      type: Array,
      default: () => []
    },
    options: {
      type: Object,
      default: () => {}
    }
  },
  mounted () {
    this.sliderInit();
  },
  methods: {
    sliderInit () {
      if (this.options) {
        $(`.${this.sliderClass}`).slick(this.options);
      } else {
        $(`.${this.sliderClass}`).slick();
      }
    }
  }
}
</script>

<style lang="scss">
.slick-prev:before,
 .slick-next:before {
  color: grey;
}
</style>