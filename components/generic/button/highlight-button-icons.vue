<template>
  <div class="icon-container">
    <slot name="icon">
      <div :class="`name-${icon}`" class="icon">
        <template v-if="icon === 'arrow'">
          <svg
            version="1.1"
            xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink"
            x="0px"
            y="0px"
            viewBox="0 0 50 50"
            style="enable-background:new 0 0 50 50;"
            xml:space="preserve"
          >
            <line class="ls" x1="16.618" y1="7.895" x2="33.382" y2="25" />
            <line class="ls" x1="16.618" y1="42.105" x2="33.382" y2="25" />
          </svg>
        </template>
        <template v-if="icon === 'tail-arrow-right'">
          <svg
            version="1.1"
            xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink"
            x="0px"
            y="0px"
            viewBox="0 0 50 50"
            style="enable-background:new 0 0 50 50;"
            xml:space="preserve"
          >
            <line class="ls" x1="27.952" y1="13.486" x2="39.349" y2="25.116" />
            <line class="ls" x1="27.952" y1="36.746" x2="39.349" y2="25.116" />
            <line class="ls" x1="38.651" y1="25.116" x2="10.651" y2="25.116" />
          </svg>
        </template>
        <template v-if="icon === 'tail-arrow-down'">
          <svg
            version="1.1"
            id="Layer_1"
            xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink"
            x="0px"
            y="0px"
            viewBox="0 0 50 50"
            style="enable-background:new 0 0 50 50;"
            xml:space="preserve"
          >
            <line class="ls" x1="36.63" y1="28.068" x2="25" y2="39.465" />
            <line class="ls" x1="13.37" y1="28.068" x2="25" y2="39.465" />
            <line class="ls" x1="25" y1="38.767" x2="25" y2="10.767" />
          </svg>
        </template>
        <template v-if="icon === 'triangle-right'">
          <svg
            version="1.1"
            xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink"
            x="0px"
            y="0px"
            viewBox="0 0 50 50"
            style="enable-background:new 0 0 50 50;"
            xml:space="preserve"
          >
            <polygon class="pf" points="14.849,8.987 14.849,39.678 36.072,24.332 " />
          </svg>
        </template>
        <template v-if="icon === 'external-link'">
          <svg
            version="1.1"
            xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink"
            x="0px"
            y="0px"
            viewBox="0 0 50 50"
            style="enable-background:new 0 0 50 50;"
            xml:space="preserve"
          >
            <g>
              <polyline
                class="ls"
                points="44.157,32 44.157,44.157 5.843,44.157 5.843,5.843 18,5.843 	"
              />
              <line class="ls" x1="25" y1="25" x2="44.157" y2="5.843" />
              <line class="ls" x1="32" y1="5.843" x2="44.157" y2="5.843" />
              <line class="ls" x1="44.157" y1="18" x2="44.157" y2="5.843" />
            </g>
          </svg>
        </template>
        <template v-if="icon === 'loading-circle'">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="100"
            height="100"
            viewBox="0 0 100 100"
            class="loading"
          >
            <circle class="cr" cx="50" cy="50" r="40" />
          </svg>
        </template>
        <template v-if="icon === 'loading-circle-gradient'">
          <div class="loading-circle-gradient"></div>
        </template>
        <template v-if="icon === 'phone'">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 27.107 27.238">
            <path
              class="sf"
              d="M31.95,12.064,28.7,15.446a2.124,2.124,0,0,0,0,3.122l2.6,2.6a21.713,21.713,0,0,1-9.366,9.366l-2.6-2.6a2.124,2.124,0,0,0-3.122,0l-3.382,3.252a2.55,2.55,0,0,0,0,3.252L16.21,37.69C21.8,43.414,44.048,21.04,38.454,15.446L35.2,12.064A2.276,2.276,0,0,0,31.95,12.064Z"
              transform="translate(-12.242 -11.381)"
            />
          </svg>
        </template>
      </div>
    </slot>
  </div>
</template>

<script>
export default {
  name: "HighlightButtonIcon",
  props: {
    icon: {
      type: String,
      required: true,
    },
  },
};
</script>

<style lang="scss">
.highlight-link {
  //ls = line-stroke class
  //pf = poly fill class
  //sf = standard fill
  //cr = gradient circle
  .ls,
  .pf {
    @include transition((fill 0.3s, color 0.3s, stroke 0.3s));
  }
  .ls {
    fill: transparent;
    stroke: var(--vc-highlight-action-icon-color);
    stroke-width: 7;
    stroke-linecap: round;
    stroke-linejoin: round;
    stroke-miterlimit: 10;
  }
  .pf {
    fill: var(--vc-highlight-action-icon-color);
    stroke: var(--vc-highlight-action-icon-color);
    stroke-width: 7;
    stroke-linecap: round;
    stroke-linejoin: round;
    stroke-miterlimit: 10;
  }

  .sf {
    fill: var(--vc-highlight-action-icon-color);
  }
  .cr {
    stroke-width: 15;
    transform-box: fill-box;
    transform-origin: center;
    fill: transparent;
    stroke-dasharray: 90; //dash array as fallback, there's a reall strange issue with using defs + gradient stops
    stroke: var(--vc-highlight-action-icon-color);
  }

  .cr {
    animation: rotate 1s infinite linear;
  }

  .loading-circle-gradient {
  }
}

@keyframes rotate {
  100% {
    transform: rotate(360deg);
  }
}
</style>