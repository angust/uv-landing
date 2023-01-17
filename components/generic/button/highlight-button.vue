<template>
  <a
    :href="url"
    class="highlight-link"
    :class="[
      getButtonType,
      getButtonStyle,
      getIconPosition,
      getButtonSize,
      getBlock,
    ]"
    :target="targetNewWindow"
    :rel="buttonRel"
  >
    <template v-if="slotIconUsed">
      <div class="icon-container">
        <slot name="slotIcon"></slot>
      </div>
    </template>

    <template v-if="hasIcon(icon)">
      <highlight-button-icons :icon="icon" />
    </template>
    <span v-if="title">{{ title }}</span>
  </a>
</template>

<script>
import HighlightButtonIcons from "./highlight-button-icons.vue";

export default {
  components: {
    HighlightButtonIcons,
  },
  name: "HighlightButton",
  props: {
    buttonType: {
      type: String,
      default: "square",
      required: false,
      validator: (prop) =>
        ["pill", "rounded", "square", "text", "text-underline", "default"].includes(prop),
    },
    buttonStyle: {
      type: String,
      default: "solid",
      required: false,
      validator: (prop) => ["solid", "outline"].includes(prop),
    },
    url: {
      type: String,
      required: false,
    },
    block: {
      type: Boolean,
      required: false,
    },
    title: {
      type: String,
      required: false,
    },
    urlNewWindow: {
      type: Boolean,
      default: false,
      required: false,
    },
    icon: {
      type: String,
      required: false,
      default: null,
      validator: (prop) =>
        [
          "tail-arrow-right",
          "tail-arrow-down",
          "arrow",
          "triangle-right",
          "phone",
          "external-link",
        ].includes(prop),
    },
    iconPosition: {
      type: String,
      required: false,
      default: "right",
      validator: (prop) => ["left", "right"].includes(prop),
    },
    buttonSize: {
      type: String,
      required: false,
      default: "standard",
      validator: (prop) => ["small", "standard", "large"].includes(prop),
    },
    buttonWidth: {
      type: String,
      required: false,
    },
  },

  methods: {
    hasIcon() {
      if (this.icon != null && this.icon) {
        return true;
      } else {
        return false;
      }
    },
  },
  computed: {
    slotIconUsed() {
      return !!this.$slots.slotIcon;
    },
    getBlock() {
      return {
        "highlight-link-block": this.block,
      };
    },
    targetNewWindow() {
      if (this.urlNewWindow != null && this.urlNewWindow) {
        return "_blank";
      } else {
        return "_self";
      }
    },
    buttonRel() {
      if (this.urlNewWindow != null && this.urlNewWindow) {
        return "noreferrer";
      } else {
        return null;
      }
    },
    getButtonType() {
      if (this.buttonType === "default") {
        return "highlight-link-default";
      }
      if (this.buttonType === "text") {
        return "highlight-link-text";
      }
      if (this.buttonType === "text-underline") {
        return "highlight-link-text underline";
      }
      if (this.buttonType === "square") {
        return "highlight-link-button square";
      }
      if (this.buttonType === "rounded") {
        return "highlight-link-button rounded";
      }
      if (this.buttonType === "pill") {
        return "highlight-link-button pill";
      }
    },
    getButtonStyle(getButtonType) {
      if (
        getButtonType !== null &&
        this.buttonStyle === "solid" &&
        this.buttonType != "text"
      ) {
        return "solid";
      }
      if (
        getButtonType !== null &&
        this.buttonStyle === "outline" &&
        this.buttonType != "text"
      ) {
        return "outlined";
      }
      return null;
    },
    getButtonSize() {
      if (this.buttonSize != null && this.buttonSize) {
        return `highlight-link-size-${this.buttonSize}`;
      }
      return null;
    },
    getIconPosition(displaySlotIcon) {
      if (
        (this.icon !== null || this.slotIconUsed) &&
        this.iconPosition === "left"
      ) {
        return "highlight-link-icon-left";
      }
      if (
        (this.icon !== null || this.slotIconUsed) &&
        this.iconPosition === "right"
      ) {
        return "highlight-link-icon-right";
      }

      return null;
    },
  },
};
</script>

<style lang="scss" scoped>
//!note vincreative projects will need the  @import '~@scss/custom.scss'; to make use of mixins and media queries

//inherit styling
.highlight-link {
  /*  --vc-highlight-action-background-color: var(--vc-accent-color);
    --vc-highlight-action-text-color: var(--vc-light-color);
    --vc-highlight-action-icon-color: var(--vc-highlight-action-text-color);
    --vc-highlight-action-outline-text-color: var(--vc-accent-color);
    --vc-highlight-action-outline-color: var(--vc-accent-color);
    --vc-highlight-action-outline-hover-text-color: var(--vc-light-color);
    --vc-highlight-action-outline-hover-color: var(--vc-accent-contrast-color);
    --vc-highlight-action-size:1em;
    --vc-highlight-action-icon-color: var(--vc-highlight-action-text-color);

    --vc-highlight-action-outline-hover-text-color: var(--vc-light-color);
    --vc-highlight-action-outline-hover-color: var(--vc-accent-contrast-color);  */

  --highlight-button-border-radius: 3px;
  --vc-highlight-action-size: 1em;
}

.highlight-link {
  ::v-deep .icon {
    width: 1em;
    height: 1em;
    display: flex;

    svg {
      width: 100%;
      height: 100%;
    }

    .st0 {
      fill: none;
      stroke-width: 8;
      stroke-linecap: round;
      stroke-linejoin: round;
      stroke-miterlimit: 10;
    }
  }
  &-icon-left {
    justify-content: space-between; //we push the icons and text to each side overrideing center text alignment on the default button position
    .icon-container {
      margin-right: 0.75em;
    }
  }
  &-icon-right {
    justify-content: space-between;
    flex-direction: row-reverse;
    .icon-container {
      &:not(:only-child) {
        margin-left: 0.75em;
      }
    }
  }
  .icon-container {
    transition: transform 0.3s;
  }
  &:disabled {
    cursor: default;
  }
}

//shared
.highlight-link-text,
.highlight-link-button {
  display: inline-flex;
  line-height: 1;
  word-break: break-word;
  cursor: pointer;
  @include transition(
    (transform 0.3s, background 0.3s, color 0.3s, box-shadow 0.3s)
  );
  font-size: var(--feature-highlight-action-font-size);
  font-family: var(--feature-highlight-action-font-family);
  .icon {
    @include transition((fill 0.3s, color 0.3s, stroke 0.3s));
  }
  @include hover-focus {
    transform: translateY(-0.4em);
  }
}

//text version
.highlight-link-text {
  position: relative;
  color: var(--vc-link-color);
  text-decoration: none;
  border: none;
  background: none;
  &.underline {
    &:after {
      content: "";
      position: absolute;
      left: 0;
      bottom: -0.4em;
      height: 2px;
      width: 100%;
      background: var(--vc-link-color);
      z-index: 0;
      transition: height 0.25s cubic-bezier(0.6, 0, 0.4, 1);
    }
  }
  ::v-deep .icon {
    --vc-highlight-action-icon-color: var(--vc-link-color);
  }

  @include hover-focus {
    color: var(--vc-link-hover-color);
    ::v-deep .icon {
      --vc-highlight-action-icon-color: var(--vc-link-color);
    }
  }
}
//button
.highlight-link-button {
  padding: .75em 1.5em;
  text-decoration: none;
  border: none;
  justify-content: center;
  line-height: 1.25;
  align-items: center;
  &:focus {
    outline: none;
    box-shadow: 0 0 0 4px rgba(0, 0, 0, 0.25); //make variable
  }

  //button type, I know this might be confusing as text, is currently a type as well.. :S
  &.square {
    border-radius: 0px;
  }

  &.rounded {
    border-radius: var(--highlight-button-border-radius);
  }

  &.pill {
    border-radius: 4em;
  }

  //button styles
  &.solid {
    color: var(--vc-highlight-action-text-color);
    position: relative;
    overflow: hidden;
    background-color: var(--vc-highlight-action-background-color);
    border: 2px solid;
    border-color: var(--vc-highlight-action-background-color);

    ::v-deep .icon {
      --vc-highlight-action-icon-color: var(--vc-highlight-action-text-color);
    }

    @include hover-focus {
      color: var(--vc-highlight-action-text-color);
      &:before {
        opacity: 0.9;
      }
    }
  }

  &.outlined {
    background: transparent;
    color: var(--vc-highlight-action-outline-text-color);
    border: 2px solid;
    border-color: var(--vc-highlight-action-outline-color);
    ::v-deep .icon {
      --vc-highlight-action-icon-color: var(
        --vc-highlight-action-outline-text-color
      );
    }
    @include hover-focus {
      background: var(--vc-highlight-action-outline-hover-color);
      border-color: var(--vc-highlight-action-outline-hover-color);
      color: var(--vc-highlight-action-outline-hover-text-color);
      ::v-deep .icon {
        --vc-highlight-action-icon-color: var(
          --vc-highlight-action-outline-hover-text-color
        );
      }
    }
  }
}

.highlight-link-size-small {
  font-size: calc(var(--vc-highlight-action-size) * 0.8);
}
.highlight-link-size-standard {
  font-size: var(--vc-highlight-action-size);
}
.highlight-link-size-large {
  font-size: calc(var(--vc-highlight-action-size) * 1.25);
}

.highlight-link-block {
  flex: 1;
  width: 100%;
  justify-content: space-between;
  & > *:only-child {
    margin: auto;
  }
}
</style>