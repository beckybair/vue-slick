<template>
  <div class="hello container">
    <h1>{{ msg }}</h1>
    <p>based off of: <a href="https://github.com/kenwheeler/slick">Slick</a> slider created by Ken Wheeler</p>
    <h2>Slider examples</h2>

    <hr class="my-3">
    <div class="sliderContainer mx-auto">
      <h3>Single Slider</h3>
      <Slider slider-class="singleSlider">
        <img v-for="(slide, sIndex) in slides" :key="sIndex" :src="slide.src" class="img-fluid" />
      </Slider>
    </div>

    <hr class="my-3">
    <div class="sliderContainer mx-auto">
      <h3>Multiple Items</h3>
      <Slider slider-class="multipleSlider" :options="multipleOptions">
        <img v-for="(slide, sIndex) in slides" :key="sIndex" :src="slide.src" class="img-fluid" />
      </Slider>
    </div>

    <hr class="my-3">
    <div class="sliderContainer mx-auto">
      <h3>Responsive Display</h3>
      <Slider slider-class="responsiveSlider" :options="responsiveOptions">
        <img v-for="(slide, sIndex) in slides" :key="sIndex" :src="slide.src" class="img-fluid" />
      </Slider>
    </div>

    <hr class="my-3">
    <div class="sliderContainer mx-auto">
      <h3>Variable Width</h3>
      <Slider slider-class="variableWidthSlider" :options="variableWidthOptions">
        <img v-for="(slide, sIndex) in slides" :key="sIndex" :src="slide.src" class="img-fluid" />
      </Slider>
    </div>

    <hr class="my-3">
    <div class="sliderContainer mx-auto">
      <h3>Adaptive Height</h3>
      <Slider slider-class="adaptiveHeightSlider" :options="adaptiveHeightOptions">
        <img v-for="(slide, sIndex) in slides" :key="sIndex" :src="slide.src" class="img-fluid" />
      </Slider>
    </div>

    <hr class="my-3">
    <div class="sliderContainer mx-auto">
      <h3>Slider Syncing</h3>
      <Slider slider-class="sliderSyncingForSlider" :options="sliderSyncingForOptions">
        <img v-for="(slide, sIndex) in slides" :key="sIndex" :src="slide.src" class="img-fluid" />
      </Slider>
      <div class="mt-4">
        <Slider slider-class="sliderSyncingNavSlider" :options="sliderSyncingNavOptions">
          <img v-for="(slide, sIndex) in slides" :key="sIndex" :src="slide.src" class="img-fluid" />
        </Slider>
      </div>
    </div>

    <hr class="my-3">
    <h3>Vertical Slider Syncing</h3>
    <button class="btn btn-secondary" @click="zoomOn = !zoomOn">{{ zoomOn ? 'Zoom Off' : 'Zoom On' }}</button>
    <div class="sliderContainer mx-auto row col-12">
      <div class="col-4">
        <Slider slider-class="sliderSyncingNavVerticalSlider" :options="sliderSyncingNavVerticalOptions">
          <img v-for="(slide, sIndex) in slides" :key="sIndex" :src="slide.src" class="img-fluid" />
        </Slider>
      </div>
      <div class="col-8 my-auto">
        <span :class="{ 'd-none': !zoomOn }">
          <Slider slider-class="sliderSyncingForVerticalSlider" :options="sliderSyncingForVerticalOptions">
            <zoom-on-hover
              v-for="(slide, sIndex) in slides"
              :key="sIndex"
              :img-normal="slide.src"
              img-alt="testing alt"
              img-class="img-fluid"
              scale="2"
            />
          </Slider>
        </span>
        <span :class="{ 'd-none': zoomOn }">
          <Slider slider-class="sliderSyncingForVerticalSlider" :options="sliderSyncingForVerticalOptions">
            <img v-for="(slide, sIndex) in slides" :key="sIndex" :src="slide.src" class="img-fluid" />
          </Slider>
        </span>
      </div>
    </div>
    <footer class="mt-5">Footer goes here</footer>
  </div>
</template>

<script>
import Slider from './slickSlider/Slider'
import ZoomOnHover from './zoom/ZoomOnHover'

export default {
  name: 'HelloWorld',
  components: { Slider, ZoomOnHover },
  props: {
    msg: String
  },
  data () {
    return {
      zoomOn: false,
      slides: [
        {src: 'https://source.unsplash.com/collection/993239/600x400'},
        {src: 'https://source.unsplash.com/collection/1673600/600x400'},
        {src: 'https://source.unsplash.com/collection/1513994/600x400'},
        {src: 'https://source.unsplash.com/collection/502925/600x400'},
        {src: 'https://source.unsplash.com/collection/1891993/600x400'}
      ],
      multipleOptions: {
        infinite: true,
        slidesToShow: 3,
        slidesToScroll: 3,
        dots: true
      },
      responsiveOptions: {
        dots: true,
        infinite: false,
        speed: 300,
        slidesToShow: 4,
        slidesToScroll: 4,
        responsive: [
          {
            breakpoint: 1024,
            settings: {
              slidesToShow: 3,
              slidesToScroll: 3,
              infinite: true,
              dots: true
            }
          },
          {
            breakpoint: 600,
            settings: {
              slidesToShow: 2,
              slidesToScroll: 2
            }
          },
          {
            breakpoint: 480,
            settings: {
              slidesToShow: 1,
              slidesToScroll: 1
            }
          }
          // You can unslick at a given breakpoint now by adding:
          // settings: "unslick"
          // instead of a settings object
        ]
      },
      variableWidthOptions: {
        dots: true,
        infinite: true,
        speed: 300,
        slidesToShow: 1,
        centerMode: true,
        variableWidth: true
      },
      adaptiveHeightOptions: {
        dots: true,
        infinite: true,
        speed: 300,
        slidesToShow: 1,
        adaptiveHeight: true
      },
      sliderSyncingForOptions: {
        slidesToShow: 1,
        slidesToScroll: 1,
        arrows: false,
        fade: true,
        asNavFor: '.sliderSyncingNavSlider'
      },
      sliderSyncingNavOptions: {
        slidesToShow: 3,
        slidesToScroll: 1,
        asNavFor: '.sliderSyncingForSlider',
        dots: true,
        centerMode: true,
        focusOnSelect: true
      },
      sliderSyncingForVerticalOptions: {
        slidesToShow: 1,
        slidesToScroll: 1,
        arrows: false,
        fade: true,
        asNavFor: '.sliderSyncingNavVerticalSlider'
      },
      sliderSyncingNavVerticalOptions: {
        slidesToShow: 3,
        slidesToScroll: 1,
        asNavFor: '.sliderSyncingForVerticalSlider',
        dots: true,
        centerMode: true,
        focusOnSelect: true,
        vertical: true
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
a {
  color: #42b983;
}
.sliderContainer {
  width: 75%;
  height: auto;
}
</style>
