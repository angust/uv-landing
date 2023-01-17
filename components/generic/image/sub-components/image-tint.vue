<template>
  <div
    class="image-tint"
    :class="getTintStyle"
    :style="{ opacity: tintStrength / 100 }"
  />
</template>
<script>
export default {
  name: "ImageTint",
  props: {
    tintStyle: {
      type: String,
      default: "dark",
      required: false,
      validator: (prop) => ["dark", "blend", "vignette"].includes(prop),
    },
    tintStrength: {
      type: Number,
      default: 0,
      required: false,
      min: 0,
      max: 100,
    },
    zIndex: {
      type: Number,
      default: 3,
      required: false,
    },
  },
  computed: {
    getTintStyle() {
      return `image-tint-${this.tintStyle}`;
    },
  },
};
</script>

<style lang="scss" scoped>
//some notes on this:
//we're going to assume you know that this would need to be contained in a position relative and probably overflow hidden component
//as a generic component, z-index is a little tricky when no indexing standard has been adopted
//it's not possible to easily guess what it could be, it should be up to the parent componet to dictate this

//tint process
.image-tint {
  width: 100%;
  height: 100%;
  position: absolute;
  left: 0;
  right: 0;
  z-index: 3;
  transition: opacity 0.3s ease-in-out;
  pointer-events: none;
}
.image-tint-dark {
  background-color: var(--neutral-tint, #000);
}
.image-tint-blend {
  background-color: var(--vc-background-color);
  mix-blend-mode: overlay; //color mix blend mode at 100% opacity on safari makes the image invisible, 3.6 Roentgens
}
.image-tint-vignette {
  background: radial-gradient(transparent, var(--neutral-tint, #000)),
    transparent;
}
</style>