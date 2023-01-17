  
<template>
  <div class="grid grid-gap" :style="[displayGridItemMinWidth, displayGridGap]">
    <div class="grid-item" v-for="(item, index) in items" :key="index">
      <slot name="item" :item="{ ...item, index }" />
    </div>
  </div>
</template>
<script>
export default {
  name: "dynamic-grid",
  props: {
    items: {
      type: Array,
      required: true,
    },
    gridGap: {
      type: Number,
      required: true,
      default: 1,
      validator: function (value) {
        return value >= 0;
      },
    },
    gridItemWidth: {
      type: Number,
      default: 400,
      required: false,
    },
  },

  computed: {
    displayGridItemMinWidth() {
      return {
        "--grid-min": this.gridItemWidth + "px",
      };
    },
    displayGridGap() {
      return {
        "--grid-gap": this.gridGap + "em",
      };
    },
  },
};
</script>

<style  lang="scss" scoped>
//we define CSS max() and min() functions to fix sass compiler for being stubborn and erroring out now that browsers are using math functions
@function max($numbers...) {
  @return m#{a}x(#{$numbers});
}
@function min($numbers...) {
  @return m#{i}n(#{$numbers});
}
.grid {
  //variable defaults in case methods fail to return values
  --default-grid-gap: 1em;
  --default-grid-min: 300px;

  --gap: var(--grid-gap, var(--default-grid-gap));
  --grid-item-min-width: var(--grid-min, var(--default-grid-min));

  display: grid;
  width: 100%;
  grid-template-columns: repeat(
    auto-fill,
    minmax(var(--grid-item-min-width), 1fr)
  );

  //if support for min() fails, we force 100% columns at tiny sizes to deal with --grid-min-width values that extend beyond the width provided which will result in an overflow
  @supports not (width: min(10vw, 100px)) {
    @include media-breakpoint-down(xs) {
      grid-template-columns: repeat(auto-fill, minmax(100%, 1fr));
    }
  }

  //this solution attempts to deal with ege support where minmax isn't supported
  //we do a generic @support check to test if the browser has min math functions available a more detailed support with the minmax inside grid-template-columns fails silently
  @supports (width: min(10vw, 100px)) {
    grid-template-columns: repeat(
      auto-fill,
      minmax(min(var(--grid-item-min-width), 100%), 1fr)
    );
  }

  //overflow hidden for browsers without minmax
  overflow: hidden;
  width: 100%;

  &-gap {
    gap: var(--gap);
    grid-gap: var(--gap);

    @include media-breakpoint-up(md) {
      gap: calc(var(--gap) * 1.25);
      grid-gap: calc(var(--gap) * 1.25);
    }
    @include media-breakpoint-up(xl) {
      gap: calc(var(--gap) * 1.5);
      grid-gap: calc(var(--gap) * 1.5);
    }
  }
}
</style>




