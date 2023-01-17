<template>
  <div class="image-container-outer">
    <div class="image-container" :class="[aspectRatio]">
      <slot name="image-content-layer"></slot>
      <slot name="image-attribution-overlay"></slot>
      <div class="image-inner">
        <image-tint :tint-strength="imageTintStrength" tint-style="dark" />
        <image-parallax :speed="0.25" :offset-start="300">
          <img
            :src="source"
            class="image"
            :class="[objectFitDisplay, objectPositionDisplay]"
            :alt="alt"
            :title="title"
            rel="preload"
          />
        </image-parallax>
      </div>
      <slot name="image-attribution-footer"></slot>
    </div>
  </div>
</template>

<script>
import ImageTint from "~/components/generic/image/sub-components/image-tint.vue";
import ImageParallax from "~/components/generic/image/image-parallax.vue";

export default {
  name: "StandardImageParallax",
  components: {
    ImageTint,
    ImageParallax,
  },
  props: {
    source: {
      type: String,
      required: false,
    },
    alt: {
      type: String,
      required: false,
    },
    title: {
      type: String,
      required: false,
    },
    //aspect ratio
    aspect: {
      type: String,
      required: false,
      validator: (prop) =>
        [
          "21-9",
          "16-10",
          "16-9",
          "9-16",
          "1-1",
          "4-3",
          "3-4",
          "3-2",
          "fluid",
          null,
        ].includes(prop),
    },
    objectPosition: {
      type: String,
      required: false,
      default: "center",
      validator: (prop) =>
        [ "top",
          "bottom",
          "center",
          "left",
          "left-bottom",
          "left-top",
          "right",
          "right-bottom",
          "right-top",
          null,
        ].includes(prop),
    },
    objectFit: {
      type: String,
      required: false,
      default: "cover",
      validator: (prop) => ["cover", "contain"].includes(prop),
    },
    //tint component
    imageTintStrength: {
      type: Number,
      required: false,
      default: 0,
      min: 0,
      max: 100,
    },
  },
  methods: {},
  computed: {
    aspectRatio() {
      if (this.aspect !== "fluid" && this.aspect !== null) {
        return `aspect-ratio aspect-ratio-${this.aspect}`;
      }
      return "aspect-ratio-fluid";
    },
    objectPositionDisplay() {
      return `object-${this.objectPosition}`;
    },
    objectFitDisplay() {
      return `object-${this.objectFit}`;
    },
  },
};
</script>

<style lang="scss" scoped>
.object-cover {
  object-fit: cover;
}
.object-contain {
  object-fit: contain;
}
//meh
// xy coordinates are a better solution to this, but if tthe position adjustments are done via a dropdown then this will have to do

.object-bottom {
  object-position: bottom;
}
.object-center {
  object-position: center;
}
.object-left {
  object-position: left;
}
.object-left-bottom {
  object-position: left bottom;
}
.object-left-top {
  object-position: left top;
}
.object-right {
  object-position: right;
}
.object-right-bottom {
  object-position: right bottom;
}
.object-right-top {
  object-position: right top;
}
.object-top {
  object-position: top;
}

//aspect ratio mixins
@mixin responsive-ratio($x, $y, $pseudo: false) {
  $padding: unquote(($y / $x) * 100 + "%");
  @if $pseudo {
    &:before {
      @include pseudo($pos: relative);
      width: 100%;
      padding-bottom: $padding;
    }
  } @else {
    padding-bottom: $padding;
  }
}

//aspect ratios
.aspect-ratio {
  .image-inner {
    height: 0;
    padding: 0;
  }
}
.aspect-ratio-21-9 {
  .image-inner {
    @include responsive-ratio(21, 9);
  }
}
.aspect-ratio-16-10 {
  .image-inner {
    @include responsive-ratio(16, 10);
  }
}
.aspect-ratio-16-9 {
  .image-inner {
    @include responsive-ratio(16, 9);
  }
}
.aspect-ratio-9-16 {
  .image-inner {
    @include responsive-ratio(9, 16);
  }
}
.aspect-ratio-3-2 {
  .image-inner {
    @include responsive-ratio(3, 2);
  }
}
.aspect-ratio-4-3 {
  .image-inner {
    @include responsive-ratio(4, 3);
  }
}
.aspect-ratio-3-4 {
  .image-inner {
    @include responsive-ratio(3, 4);
  }
}
.aspect-ratio-1-1,
.aspect-ratio-square {
  .image-inner {
    @include responsive-ratio(1, 1);
  }
}

.image-container {
  width: 100%;
}
.image-inner {
  position: relative;
  width: 100%;
}
.image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
