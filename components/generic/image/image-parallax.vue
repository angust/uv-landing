<template>
  <div
    class="image-parallax"
    ref="parallax"
    :class="{
      'parallax-disabled': parallaxDisabled,
      'parallax-scrolldown': scrollDown,
      'in-focus': isIntersecting,
    }"
  >
    <div class="image-parallax-inner" ref="parallaxInner" :style="transform">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  name: "AParallax",
  props: {
    parallaxDisabled: {
      type: Boolean,
      default: false,
    },
    //inverts scroll direction
    scrollDown: {
      type: Boolean,
      default: false,
    },
    speed: {
      type: Number,
      default: 0.25,
      min: 0,
      max: 1,
    },
    //positive value, starts the movement early, negative starts after top point
    offsetStart: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      isIntersecting: false,
      offset: 0,
      //parallaxDisabled: false,
    };
  },
  mounted() {
    if (window.IntersectionObserver) {
      const observer = new IntersectionObserver(this.observerCallback);
      observer.observe(this.parallax);
      this.scroll();
    } else {
      this.parallaxDisabled = true;
    }
  },
  computed: {
    parallax() {
      return this.$refs.parallax;
    },
    parallaxInner() {
      return this.$refs.parallaxInner;
    },
    transform() {
      if (this.parallaxDisabled) {
        return false;
      }
      return `transform: translate3d(0, ${this.offset}px, 0)`;
    },
  },
  methods: {
    observerCallback(val) {
      if (val.length === 1) {
        if (val[0].isIntersecting) {
          this.isIntersecting = true;
          if (!this.parallaxDisabled) {
            document.addEventListener("scroll", this.scroll);
          }
        } else {
          this.isIntersecting = false;
          this.offset = 0;
          document.removeEventListener("scroll", this.scroll);
        }
      }
    },
    scroll() {
      let maxDelta =
        this.parallaxInner.clientHeight - this.parallax.clientHeight;
      const top = this.parallax.getBoundingClientRect().top - this.offsetStart;
      const delta = Math.min(top, 0) * this.speed * (this.scrollDown ? -1 : 1);

      if (!this.scrollDown && Math.abs(delta) > maxDelta)
        this.offset = -maxDelta;
      else this.offset = delta;
    },
  },
};
</script>

<style lang="scss" scoped>
//disabled styling for both disabled states in the component
@mixin parallax-disabled {
  top: 0 !important;
  height: 100% !important;
  //transform: none !important;
}

.image-parallax {
  height: 100%;
  width: 100%;
  overflow: hidden;
  &.parallax-disabled {
    .image-parallax-inner {
      @include parallax-disabled;
    }
  }
}
.image-parallax-inner {
  display: flex;
  justify-content: center;
  width: 100%;

  //if print or user has prefers reduced motion on parallax is disabled
  //prefers reduced motion is usually buried in a configuration option

  @media print, (prefers-reduced-motion: reduce) {
    @include parallax-disabled;
  }
}

//we add literal garbage to test that parallax

.image-parallax {
  position: absolute;
  &.parallax-scrolldown {
    .image-parallax-inner {
      top: -35%;
    }
  }
  .image-parallax-inner {
    height: 137.5%;
    position: relative;
    .image-inner {
      height: 100%;
    }
    &.parallax-disabled {
      height: 100%;
    }
  }
}
</style>
