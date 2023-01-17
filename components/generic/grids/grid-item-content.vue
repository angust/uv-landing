<template>
    <div
      class="banner-display"
      @mouseover="hover = true"
      @mouseleave="hover = false"
      :class="[interactionState]"
    >
    <slot name="background" class="background-container"></slot>

      <div class="banner-display-inner">
        <div class="banner-content-container">
          <div
            class="banner-content"
            :class="[
              displayBannerVerticalPosition,
              displayBannerHorizontalPosition
            ]"
          >
          <div class="banner-content-inner" :class="content.BannerTextAlignment">
              <div
                class="banner-content-text"
              >
                <div v-if="content.subtitle" class="banner-sub-title">
                  <h3>{{ content.subtitle }}</h3>
                </div>
                <div v-if="content.title" class="banner-title">
                  <h1 v-html="content.title" />
                </div>
                <div
                  v-if="content.description"
                  class="banner-description"
                  v-html="content.description"
                />
  
                <div class="banner-actions" :class="moreThanOne(content.actions)" v-if="titledActions">
                  <div
                    v-for="(item, index) in content.actions"
                    :key="index"
                    class="banner-action-item"
                  >
                    <HighlightButton
                      buttonType="square"
                      :buttonSize="item.buttonSize"
                      :buttonStyle="item.buttonStyle"
                      :url="item.linkUrl"
                      :title="item.linkTitle"
                      v-if="item.linkTitle && item.linkUrl"
                    />
                  </div>
                </div>
              </div>
            </div>
            <slot name="graphic"></slot>
          </div>
        </div>
      </div>
      <template v-if="content.fullBannerLink && content.fullBannerLink.linkUrl">
        <a
          class="overlay-link"
          :href="content.fullBannerLink.linkUrl"
          :target="targetNewWindow"
          :rel="buttonRel"
        ></a>
      </template>
    </div>
  </template>
  
<script>
  import HighlightButton from "~/components/generic/button/highlight-button.vue";
  export default {
    name: "ItemContent",
    data() {
      return {
        hover: false
      };
    },
    props: {
      content: {
        type: Object,
        required: true
      }
    },
    components: {
      HighlightButton,
    },
    methods: {
      moreThanOne(item) {
        if (Object.keys(item).length > 1) {
          return "actions";
        }
      },
  
      hasItem(item) {
        return Object.keys(item).length > 0;
      },
    },
    computed: {
      displayBannerVerticalPosition() {
        if (this.content.BannerVerticalPosition && this.content.BannerVerticalPosition !== null) {
          return `${this.content.BannerVerticalPosition}`;
        }
      },
      displayBannerHorizontalPosition() {
        if (this.content.BannerHorizontalPosition && this.content.BannerHorizontalPosition !== null) {
          return `${this.content.BannerHorizontalPosition}`;
        }
      },
      interactionState() {
        if (this.hover === true) {
          return "hover-overlay";
        }
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

      titledActions() {
        var found = this.content.actions.some(
          (item, index, arr) => item.linkTitle && item.linkTitle.length > 1
        );
        if (found) {
          return true;
        } else {
          return false;
        }
      },
      //find first banner button, we may use this for a full banner link, if there's no text in the button
      primaryAction() {
        return !!this.content.actions.length ? this.content.actions[0] : null;
      },
      primaryActionLinkOnly() {
        if (this.primaryAction.linkUrl && !this.primaryAction.linkTitle) {
          return true;
        }
      }, 
    },
  };
  </script>
  
<style lang="scss" scoped>

  //setup interaction types
  .background-container {
    transform:scale(1);
    transition: transform .3s ease-in-out;
  }
/* .hover-overlay {
  .background-container {
    transform:scale(1.05);
  }
} */

.banner-display {
  display: grid;
  position: relative;
  height: 100%;
  overflow: hidden; //prevent grid break when text exceeds width eg. single long words 
  --main-banner-element-margin: .5rem;
  --overlay-link-z-index: 5;
  --banner-content-text-z-index: 6;
  --banner-content-link-z-index: 7;
  --main-banner-content-text-color: white;
  --main-banner-content-title-text: white;
  --main-banner-title: 1.8em;
  --main-banner-title-font-weight:400;
  --main-banner-title-line-height:1.2;

  --main-banner-sub-title: 1.1em;
  --main-banner-sub-title-font-weight:400;
  --main-banner-description-font-size:.867em;
  --main-banner-description-line-height:1.6;
  --banner-content-inner-padding: 1.5em;
  --banner-content-inner-width: 500px; //max width of content with an individual item
}
.background-container {
  display: grid;
  grid-area: 1/1;
  z-index: 1;
}

.overlay-link {
  z-index: var(--overlay-link-z-index);
  position: absolute;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
}

.banner-display-inner {
  display: flex;
  grid-area: 1 / 1;
  padding: var(--banner-content-inner-padding);
}

//banner text
.banner-text-center {
  text-align: center;
  justify-content: center;
  align-items: center;
}

@include media-breakpoint-up(sm) {
  .banner-text-right {
    text-align: right;
    justify-content: flex-end;
  }

  .banner-text-left {
    text-align: left;
    justify-content: flex-start;
  }
}

.banner-content-container {
  width: 100%;
}
.banner-content {
  display: flex;
  flex-direction: column;
  height: 100%;
  z-index: var(--content-z-index);
  color: var(--main-banner-content-text-color);
}
.banner-content-inner {
  max-width: var(--banner-content-inner-width);
}


//typograpy and text display
.banner-sub-title h3,
.banner-title h1 {
  margin: 0;
}
.banner-sub-title h3 {
  font-size: var(--main-banner-sub-title);
  font-weight: var( --main-banner-sub-title-font-weight);
  line-height: var(--main-banner-title-line-height);
}

.banner-title h1 {
  font-size: var(--main-banner-title);
  line-height: var(--main-banner-title-line-height);
  font-weight: var( --main-banner-title-font-weight);
}
.banner-description {
    //addresses edge case for any links that could be used inside the description text area over the top of a full banner link
    font-size: var(--main-banner-description-font-size);
    line-height: var(  --main-banner-description-line-height);
    ::v-deep a {
      color: var(--main-banner-content-text-color);
      z-index: var(--banner-content-link-z-index);
      text-decoration: underline;
      position: relative;
      pointer-events: all;
    }
  }

.banner-content-text {
  display: flex;
  flex-direction: column;
  position: relative;
  z-index: var(--banner-content-text-z-index);
  pointer-events: none;
  width: 100%;

  .banner-actions {
    gap: 1em;
    display: flex;
    ::v-deep a,
    ::v-deep .highlight-link {
      z-index: var(--banner-content-link-z-index);
      position: relative;
      pointer-events: all;
    }
  }

  >*+* {
    margin-top: var(--main-banner-element-margin);
  }
}

//vertical
.banner-content-vertical {
  &-position-bottom {
    justify-content: flex-end;
  }

  &-position-centered,
  &-position-center {
    justify-content: center;
  }

  &-position-top {
    justify-content: flex-start;
  }
}

//horizontal
.banner-content-horizontal {
  &-position-left {
    align-items: flex-start;

    .banner-content-inner {
      align-items: flex-start;
    }
  }
  &-position-right {
    align-items: flex-end;
    .banner-content-inner {
      align-items: flex-end;
    }
  }

  &-position-center,
  &-position-centered {
    align-items: center;

    .banner-content-inner {
      align-items: center;
    }
  }
}
</style>