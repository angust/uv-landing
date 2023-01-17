  
<template>
  <div class="grid" :style="[displayGridGap, displayGridColumns]">
    <div class="grid-item" v-for="(item, index) in items" :key="index" :class="displayGridItemClass">
      <slot name="item" :item="{ ...item, index }" />
    </div>
  </div>
</template>
<script>
export default {
  name: "standard-grid",
  props: {
    items: {
      type: Array,
      required: true,
    },
    gridItemClass: {
      type: String,
      required:  false
    },
    gridGap: {
      type: Number,
      required: true,
      default: 1,
      validator: function (value) {
        return value >= 0;
      },
    },
    gridColumns: {
      type: Object,
      required: true,
      validator: function (payload) {
        const allowedKeys = ["small", "medium", "large"];
        const hasInvalidKeys = Object.keys(payload).some(
          (key) => !allowedKeys.includes(key)
        );
        const hasInvalidValues = Object.values(payload).some(
          (value) => typeof value !== "number"
        );
        return !hasInvalidKeys && !hasInvalidValues;
      },
    },
  },

  computed: {
    displayGridColumns() {
      return Object.keys(this.gridColumns).reduce((acc, key) => {
        acc[`--grid-${key}`] = `${this.gridColumns[key]}`;
        return acc;
      }, {});
    },
    displayGridItemClass() {
      if (this.gridItemClass !== null && this.gridItemClass) {
        return `${this.gridItemClass}`;
      }
    },
    displayGridGap() {
      return {
        "--grid-gap": `${this.gridGap}`, //css variables used instead of straight inline style values here for greater control over styling
      };
    },
  },
  methods: {},
};
</script>

<style  lang="scss" scoped>
  //imports into the vc projects will need access to media-breakpoints on this project it's globablly accessible via /assets/scss/variables.scss in the nuxt config via style resources 
.grid {
  //variable defaults in case methods fail to return values
  --default-grid-gap: 1em;
  --gap: calc(var(--grid-gap) * var(--default-grid-gap));
  --grid-size: var(--grid-small, 1);

  //setup grid
  display: grid;
  grid-template-columns: repeat(var(--grid-size), 1fr);
  grid-gap: var(--gap);
  width: 100%;
  @include media-breakpoint-up(sm) {
    --grid-size: var(--grid-small, 1);
    grid-gap: calc(var(--gap) * .75);
  }
  @include media-breakpoint-up(md) {
    --grid-size: var(--grid-medium, 3);
    grid-gap: calc(var(--gap) * 1);
  }
  @include media-breakpoint-up(lg) {
    --grid-size: var(--grid-large, 3);
    grid-gap: calc(var(--gap) * 1.25);
  }
}
.grid-item {
  //display: flex;
  grid-column: span 1;
  width: 100%;
}
</style>