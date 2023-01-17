<template>
  <div class="image-container" :class="aspectRatio">
    <div class="image-inner">
      <slot name="image-content-layer"></slot>
      <slot name="image-attribution-overlay"></slot>

      <ImageTint :tint-strength="imageTintStrength" tint-style="dark" v-if="hasImageTint"/>
      <img
        :src="source"
        class="image"
        :class="objectStyle"
        :alt="alt"
        :title="title"
        rel="preload"
        :loading="imageLazyLoad"
        
      />
    </div>
    <slot name="image-attribution-footer"></slot>
  </div>
</template>

<script>
import ImageTint from "~/components/generic/image/sub-components/image-tint.vue";

export default {
  name: "StandardImage",
  components: {
    ImageTint,
  },
  props: {
    lazyLoading: {
      type: String,
      required: false,
      validator: (prop) =>
        [
          "lazy",
          "eager",
          null,
        ].includes(prop),
    },
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
          "2-4",
          "2-3",
          "2-1",
          "1-2",
          "fluid",
          null,
        ].includes(prop),
    },
    objectPosition: {
      type: String,
      required: false,
      default: "center",
      validator: (prop) =>
        [
          "bottom",
          "center",
          "top",
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
    hasImageTint(){
      if (this.imageTintStrength > 0) {
        return true;
      }
    },
    aspectRatio() {
      if (this.aspect !== "fluid" && this.aspect !== null) {
        return `aspect-ratio aspect-ratio-${this.aspect}`;
      }
      return "aspect-ratio-fluid";
    },
    objectPositionDisplay() {
      return `object-${this.objectPosition}`;
    },
    imageLazyLoad() {
      return this.lazyLoading
    },
    objectFitDisplay() {
      return `object-${this.objectFit}`;
    },
    objectStyle(objectFitDisplay, objectPositionDisplay){
      return `${this.objectFitDisplay} ${this.objectPositionDisplay}`
    },
    fit(){
     return {
        "object-fit": `${this.objectFit}`, //css variables used instead of straight inline style values here for great control over styling
      };
    }
    
  },
};
</script>

<style lang="scss" scoped>
.image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

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

//set fallback when native aspect ratio is not supported, we check against any aspect ratio not specifically 1:1
@supports not (aspect-ratio: 1 / 1) { 
.aspect-ratio {
  .image-inner {
    height: 0;
    padding: 0;
  }
}
}
.aspect-ratio-21-9 {
  .image-inner {
    @include responsive-ratio(21, 9);
    aspect-ratio: 21 / 9;
  }
}
.aspect-ratio-16-10 {
  .image-inner {
    @include responsive-ratio(16, 10);
    aspect-ratio: 16 / 10;

  }
}
.aspect-ratio-16-9 {
  .image-inner {
    @include responsive-ratio(16, 9);
      aspect-ratio: 16 / 9;
  }
}
.aspect-ratio-9-16 {
  .image-inner {
    @include responsive-ratio(9, 16);
      aspect-ratio: 9 / 16;

  }
}
.aspect-ratio-3-2 {
  .image-inner {
    @include responsive-ratio(3, 2);
    aspect-ratio: 3 / 2;

  }
}
.aspect-ratio-2-4 {
  .image-inner {
    @include responsive-ratio(2, 4);
    aspect-ratio: 2 / 4;

  }
}
.aspect-ratio-2-3 {
  .image-inner {
    @include responsive-ratio(2, 3);
    aspect-ratio: 2 / 3;

  }
}
.aspect-ratio-4-3 {
  .image-inner {
    @include responsive-ratio(4, 3);
    aspect-ratio: 4 / 3;
  }
}
.aspect-ratio-3-4 {
  .image-inner {
    @include responsive-ratio(3, 4);
    aspect-ratio: 3 / 4;
  }
}
.aspect-ratio-2-1{
  .image-inner {
    @include responsive-ratio(2, 1);
    aspect-ratio: 2 / 1;
  }
}
.aspect-ratio-1-2{
  .image-inner {
    @include responsive-ratio(1, 2);
    aspect-ratio: 1 / 2;
  }
}
.aspect-ratio-1-1,
.aspect-ratio-square {
  .image-inner {
    @include responsive-ratio(1, 1);
    aspect-ratio: 1 / 1;
  }
}

.aspect-ratio-fluid {
  width:100%;
  height:100%;
  .image-inner {
    height:100%;
  }
}
.image-container {
  width: 100%;
  //height:100%;
}
.image-inner {
  position: relative;
  width: 100%;
  //height:100%;
}

</style>
