<template>
  <standard-image-display
    :source="source"
    :aspect="aspect"
    :object-position="objectPosition"
    :object-fit="objectFit"
    lazyLoading="lazy"
  >
    <template slot="image-content-layer">
      <slot name="image-content-layer" component="wrapperComponent"></slot>
    </template>
    <div
      slot="image-attribution-overlay"
      class="image-attribution-overlay"
      v-if="overlayAttribution && displayAttribution"
      :class="toggleAttribution.class"
    >
      <transition name="fade">
        <ContentImageInfo
          :authorName="authorName"
          :authorDescription="authorDescription"
          :authorUrl="authorUrl"
          v-if="imageInfoToggle"
        />
      </transition>
      <button
        class="action"
        @click="toggle()"
        :title="`${toggleAttribution.text} Image Attribution`"
        alt="Image Attribution"
      >
        <svg
          class="icon"
          x="0px"
          y="0px"
          viewBox="0 0 100 100"
          xml:space="preserve"
        >
          <g>
            <circle cx="50" cy="54.1" r="12.9"></circle>
            <path
              d="M91.5,28.9l-20.8-2.5l-4.4-8.9c-0.8-1.7-2.5-2.7-4.4-2.7H38.1c-1.9,0-3.6,1.1-4.4,2.7l-4.4,8.9L8.5,28.9     c-3.4,0.4-6,3.3-6,6.8v38c0,3.8,3.1,6.9,6.9,6.9h24.1c4.8,3,10.4,4.8,16.5,4.8c6.1,0,11.7-1.8,16.5-4.8h24.1     c3.8,0,6.9-3.1,6.9-6.9v-38C97.5,32.2,94.9,29.3,91.5,28.9z M21.4,44c0,1.6-1.3,2.9-2.9,2.9h-4.2c-1.6,0-2.9-1.3-2.9-2.9v-4.2     c0-1.6,1.3-2.9,2.9-2.9h4.2c1.6,0,2.9,1.3,2.9,2.9V44z M50,73.7c-10.8,0-19.6-8.8-19.6-19.6c0-10.8,8.8-19.6,19.6-19.6     c10.8,0,19.6,8.8,19.6,19.6C69.6,64.9,60.8,73.7,50,73.7z"
            ></path>
          </g>
        </svg>
      </button>
    </div>

    <div
      slot="image-attribution-footer"
      class="image-attribution-footer"
      v-if="!overlayAttribution && displayAttribution"
    >
      <ContentImageInfo
        :authorName="authorName"
        :authorUrl="authorUrl"
        :authorDescription="authorDescription"
      />
    </div>
  </standard-image-display>
</template>

<script>
import ContentImageInfo from "~/components/generic/image/content-image-info.vue";
import StandardImageDisplay from "~/components/generic/image/standard-image-display.vue";
import wrapperComponent from "~/components/wrapper-component.vue";
export default {
  components: { ContentImageInfo, StandardImageDisplay, wrapperComponent },
  name: "ContentImageAttribution",
  data() {
    return {
      imageInfoToggle: false,
    };
  },
  props: {
    source: {
      type: String,
      required: false,
    },
    alt: {
      type: String,
      required: false
    },
    title: {
      type: String,
      required: false
    },
    authorDescription: {
      type: String,
      required: false
    },
    authorName: {
      type: String,
      required: false
    },
    authorUrl: {
      type: String,
      required: false
    },
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
          "2-3",
          "2-1",
          "1-2",
          "fluid",
          null,
        ].includes(prop)
    },
    overlayAttribution: {
      type: Boolean,
      required: false,
      default: false,
    },
    objectPosition: {
      type: String,
      required: false,
      default: "center",
      validator: (prop) =>
        [
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
  },
  methods: {
    toggle: function () {
      this.imageInfoToggle = !this.imageInfoToggle;
    },
  },
  computed: {
    toggleAttribution() {
      let state = this.toggle;
      if (this.imageInfoToggle === true) {
        state = {
          value: true,
          class: "overlay-active",
          text: "Hide",
        };
      } else {
        state = {
          value: false,
          class: null,
          text: "Show",
        };
      }
      return state;
    },
    imageFullWidthDisplay() {
      let state = this.toggle;
      if (this.imageFullWidth === true) {
        state = {
          value: true,
          class: "full-width",
        };
      } else {
        state = {
          value: false,
          class: null,
        };
      }
      return state;
    },
    displayAttribution() {
      if (this.authorName || this.authorDescription) {
        return true;
      }
    },
    //show name & link of author if available
    /*     authorInfo(content) {
      if (this.content.authorName && this.content.authorUrl) {
        return `<a href="${this.content.authorUrl}" target="_blank" rel="noopener noreferrer">${this.content.authorName}</a>`;
      } else if (this.content.authorName || !this.content.authorUrl) {
        return `${this.content.authorName}`;
      }
    }, */
  },
};
</script>

<style lang="scss" scoped>
//scrim gradient
//star color should be solid, rgba start will convert back to opacity of 1 as listed in the cooordinates below
@mixin scrimGradient($direction: "to bottom", $startColor: "color") {
  $scrimCoordinates: (
    0: 1,
    19: 0.738,
    34: 0.541,
    47: 0.382,
    56.5: 0.278,
    65: 0.194,
    73: 0.126,
    80.2: 0.075,
    86.1: 0.042,
    91: 0.021,
    95.2: 0.008,
    98.2: 0.002,
    100: 0,
  );

  $hue: hue($startColor);
  $saturation: saturation($startColor);
  $lightness: lightness($startColor);
  $stops: ();

  @each $colorStop, $alphaValue in $scrimCoordinates {
    $stop: hsla($hue, $saturation, $lightness, $alphaValue)
      percentage($colorStop/100);
    $stops: append($stops, $stop, comma);
  }

  background: linear-gradient(unquote($direction), $stops);
}
.image-attribution-overlay {
  z-index: 4; //weighted above tint slot
  --image-content-background-color: rgba(0, 0, 0, 0.5);
  --image-content-icon-color: #fff;
  --image-content-inner-padding: 1.25em;
  --image-content-icon-size: 2em;
  --image-overlay-content-margin-adjustment: calc(
    var(--image-content-inner-padding) + var(--image-content-icon-size)
  );
  --image-overlay-text-color:#fff;
  --image-overlay-text-size:14px;
}
//generic image attribution

//generic image attribution position
.image-attribution-footer {
  padding-top: 1em;
  opacity: 0.5;
  text-align: center;
}

//overlay image attribution
::v-deep .image-attribution-overlay {
  color: var(--image-overlay-text-color);
  position: absolute;
  bottom: 0;
  right: 0;
  font-size: var(--image-overlay-text-size);
  display: flex;
  flex-direction: row;
  align-content: center;
  align-items: flex-end;
  width: 100%;
  height: 100%;
  justify-content: flex-end;
  overflow: hidden;
  .image-attribution-inner {
    z-index: 1;
    position: relative;
    margin-right: var(--image-overlay-content-margin-adjustment);
  }
  .image-attribution {
    display: flex;
    justify-content: flex-end;
    width: 100%;
    padding: var(--image-content-inner-padding);
    padding-top: calc(
      var(--image-content-inner-padding) * 1.5
    ); //slight increase in legibility by extending the image attribution gradient if the padding is small here
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    a {
      text-decoration: underline;
      text-decoration-line: underline;

      color: var(--image-overlay-text-color);
      &:visited {
        text-decoration-style: dotted;
      }
    }
  }

  &.overlay-active {
    .image-attribution {
      &:before {
        content: " ";
        //background: linear-gradient(180deg, transparent, rgba(0, 0, 0, 0.65));
        opacity: 0.75;
        width: 100%;
        height: 150%; //we extend height for extra readability over he scrimgradient
        left: 0;
        position: absolute;
        bottom: 0;
        @include scrimGradient("to top", #000);
      }
    }
  }
}

.content-image {
  height: auto;
  width: 100%;
}

//svg icon for image attribution

.action {
  background: transparent;
  outline: none;
  border: 0;
  margin: var(--image-content-inner-padding);
  padding: 0;
  transition: transform 0.3s ease-in-out;
  cursor: pointer;

  &:hover{
    outline: none;
    .icon {
      outline: none;
      animation-duration: 450ms;
      animation-name: shake-rotate;
      animation-iteration-count: infinite;
      animation-direction: alternate;
    }
  }
  &:active:focus {
    .icon {
      animation: none;
    }
  }
  .icon {
    transition: transform 0.3s ease-in-out;
    width: var(--image-content-icon-size);
    height: var(--image-content-icon-size);
    color: var(--image-content-icon-color);
    fill: var(--image-content-icon-color);
    filter: drop-shadow(0px 1px 3px rgba(0, 0, 0, 0.3));
    circle {
      transform-origin: center;
      transition: transform 0.3s ease-in-out;
    }
  }
}

.overlay-active {
  .action {
    .icon {
      animation: none;
      circle {
        transform: scale(0.55);
        transform-origin: 50% 54%;
        transition: transform 0.3s ease-in-out;
      }
    }
    &:hover,
    &:focus {
      transform: scale(0.9);
    }
  }
}
//animations

//fade

.fade-enter-active,
.fade-leave-active,
.fade-enter,
.fade-leave-to {
  transition: opacity 0.3s ease-in-out;
}

.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

//gentle shake

@keyframes shake-rotate {
  0% {
    transform: rotate(0deg);
  }
  25% {
    transform: rotate(15deg);
  }

  50% {
    transform: rotate(-15deg);
  }
  100% {
    transform: rotate(0deg);
  }
}

</style>
