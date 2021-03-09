<template>
  <div>
    <div>
      <nav
        class="uk-navbar uk-navbar-container uk-margin uk-position-absolute nav"
      >
        <div class="uk-navbar-right">
          <a class="uk-navbar-toggle" uk-navbar-toggle-icon href="#"></a>
        </div>
      </nav>
      <div class="uk-flex slider-columns">
        <div class="uk-width-1-2@s">
          <div
            class="uk-height-1-1 uk-flex uk-flex-column uk-flex-middle uk-flex-center"
          >
            <div class="uk-width-3-4 text-container">
              <div class="uk-flex">
                <h3 class="indexSlider animatedContent">
                  0{{ textIndex + 1 }}
                  <span>|</span>
                </h3>
                <img
                  :src="slider[textIndex].icon"
                  :alt="
                    slider[textIndex].icon.substring(
                      6,
                      slider[textIndex].icon.indexOf('.')
                    )
                  "
                  class="slide-icon"
                />
              </div>

              <h2 class="title animatedContent">
                {{ slider[textIndex].title }}
              </h2>
              <hr class="hr" />
              <div class="animatedContent">
                <p class="paragraph">
                  {{ slider[textIndex].paragraph }}
                </p>

                <div>
                  <button class="btn-primary">Saber más</button>
                </div>
              </div>
            </div>
            <div class="social-media uk-width-3-4 uk-visible@s animatedContent">
              <span uk-icon="facebook" class="uk-margin-right"></span>
              <span uk-icon="twitter" class="uk-margin-right"></span>
              <span uk-icon="instagram"></span>
            </div>
          </div>
        </div>
        <div class="slider uk-width-1-2@s" :touchable="false">
          <vueper-slides
            ref="slider"
            fixed-height="100vh"
            :arrows="false"
            :bullets="false"
            class="slider"
          >
            <vueper-slide
              v-for="(slide, indexSlider) in slider"
              :key="indexSlider"
              :image="slide.image"
            />
          </vueper-slides>
        </div>
      </div>
      <div>
        <button
          class="chevron-slide-2 animatedContent"
          @click="$refs.slider.next(), slideImage()"
        >
          <span uk-icon="icon: chevron-right; ratio: 1.5"></span>
        </button>
        <button
          class="chevron-slide-1 animatedContent"
          @click="$refs.slider.previous(), slideImage()"
        >
          <span uk-icon="icon: chevron-left; ratio: 1.5"></span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { VueperSlides, VueperSlide } from 'vueperslides'
import 'vueperslides/dist/vueperslides.css'

import { gsap } from 'gsap'
export default {
  components: {
    VueperSlides,
    VueperSlide,
  },

  data: () => ({
    textIndex: 0,
    isLoading: true,

    slider: [
      {
        icon: 'images/icons/1.svg',
        title: 'Misión',
        paragraph:
          'El veganismo no es ninguna dieta. Es una actitud de rebeldía, una postura ética basada en el profundo respeto por los animales y nuestro entorno. Ese respeto pasa por no comerlos ni usarlos para vestir o esclavizarlos para nuestro disfrute o enriquecimiento. Es un espacio en el que se da voz a quienes no la tienen.',
        image: 'images/hero-img-1.jpg',
      },
      {
        icon: 'images/icons/2.svg',
        title: 'Explora',
        paragraph:
          'The flex component has an essential role in building layouts in UIkit. A lot of components, for example the Grid as well as horizontal navigations, like the Navbar, Subnav, Breadcrumb, Pagination, Tab and Dotnav are built with flexbox and can be used together with the utility classes from this component.',
        image: 'images/hero-img-2.jpg',
      },
      {
        icon: 'images/icons/3.svg',
        title: 'Productos',
        paragraph:
          'The Zip file contains the compiled CSS and JavaScript files, which is everything you need to get started. Later, you might want to install and compile UIkit yourself and also create your own UIkit theme.',
        image: 'images/hero-img-3.jpg',
      },
    ],
  }),

  mounted() {
    const tl1 = gsap.timeline()
    const tl2 = gsap.timeline()
    const tl3 = gsap.timeline()
    tl1.fromTo(
      '.vueperslide:first-child',
      { scale: 2, opacity: 0 },
      { duration: 0.8, scale: 1, opacity: 1 }
    )
    tl2.fromTo(
      '.animatedContent',
      { y: 120, opacity: 0 },
      { duration: 0.8, y: 0, opacity: 1, delay: 0.3, stagger: 0.2 }
    )
    tl3.fromTo(
      '.hr',
      { width: 0, opacity: 0 },
      { duration: 0.8, width: '100%', opacity: 1, delay: 0.8 }
    )
  },
  methods: {
    finishLoading() {
      this.isLoading = false
    },
    slideImage() {
      this.textIndex = this.$refs.slider.slides.current
    },
  },
}
</script>

<style></style>
