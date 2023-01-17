<template>
  <div
    v-html="content"
    class="wysiwyg-content"
    :class="lineHeightDisplay"
  ></div>
</template>

<script>
export default {
  name: "WysiwygContent",
  props: {
    content: {
      type: String,
      required: true,
    },
    lineHeight: {
      type: String,
      default: "standard",
      required: false,
      validator: (prop) => ["compact", "standard", "spaced"].includes(prop),
    },
  },
  computed: {
    lineHeightDisplay() {
      return `lh-${this.lineHeight}`;
    },
  },
};
</script>

<style lang="scss">
.wysiwyg-content {
  --flow-space-value: 2;
  --flow-space-unit: 1rem;
  --flow-space: calc(var(--flow-space-value) * var(--flow-space-unit));

  --ratio: 1.333; //perfect fourth scale
  --font-size: 100%;

  /* Calculate values */
  --h4: calc(var(--font-size) * var(--ratio));
  --h3: calc(var(--h4) * var(--ratio));
  --h2: calc(var(--h3) * var(--ratio));
  --h1: calc(var(--h2) * var(--ratio));

  white-space: pre-wrap;
  word-wrap: break-word;
  color: var(--vc-text-color);
  a {
    color: var(--vc-link-color);
    text-decoration: underline;
    text-decoration-thickness: 0.1em; //spec strongly reccomends em instead of pixel based values here.
    text-underline-offset: 4px;
    transition: color 0.3s ease-in-out, text-underline-offset 0.3s ease-in-out;
    &:hover,
    &:focus {
      color: var(--vc-link-hover-color);
      text-underline-offset: 7px;
    }
  }
  h1,
  h2,
  h3,
  h4,
  h5,
  h6,
  .h1,
  .h2,
  .h3,
  .h4,
  .h5,
  .h6 {
    line-height: var(--vc-heading-line-height);
    color: var(--vc-text-heading-color);
  }

  ol,
  ul,
  dl {
    list-style-position: outside;
    padding-left: 1em;
  }
  ul {
    list-style: disc;
  }
  hr {
    border-color: var(--vc-border-color);
  }

  blockquote {
    border-left: 4px solid var(--vc-link-color);
    padding-left: 2em;
    font-style: italic;
  }

  &.lh-compact {
    line-height: calc(var(--vc-line-height) * .9);
    --flow-space-value: 1;
  }

  &.lh-standard {
    line-height: calc(var(--vc-line-height) * 1);
    --flow-space-value: 1;
  }

  &.lh-spaced {
    line-height: calc(var(--vc-line-height) * 1.2);
    --flow-space-value: 1.5;
  }

}

.wysiwyg-content > *,
.wysiwyg-content > * + * {
  &:not(:last-child) {
    margin-top: 0;
    margin-bottom: var(--flow-space);
  }
}

//wysiwyg intergation probably would need to go below
</style>