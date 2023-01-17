<template>
    <div class="content-card" 
        @mouseover="hover = true"
        @mouseleave="hover = false"
        >
        <component 
            :is="attributeType" 
            :href="content.image.url"
            :target="targetNewWindow"
            class="content-card-image-region"
            :class="attributeClass"
        >   
                <standard-image-display 
                    :alt="content.image.alt"
                    :title="content.image.title"
                    :source="content.image.filepath"
                    :object-position="content.image.objectPosition"
                    :object-fit="content.image.objectFit"
                    lazyLoading="lazy"
                    :imageTintStrength="content.image.tint"
                    :aspect="aspect" 
                    class="image-layer image-layer-1"
                />
                <template v-if="content.imageHover">
                    <transition name="fade">
                        <standard-image-display v-show="hover === true"
                            :alt="content.imageHover.alt"
                            :title="content.imageHover.title"
                            :source="content.imageHover.filepath"
                            :object-position="content.imageHover.objectPosition"
                            object-fit="cover"
                            lazyLoading="lazy"
                            :imageTintStrength="content.imageHover.tint"
                            :aspect="aspect"
                            class="image-layer image-layer-2"
                        />
                    </transition>
            </template>
        </component>
        <GridItemContent :content="content.text"/>
    </div>
</template>

<script>
import StandardImageDisplay from "~/components/generic/image/standard-image-display.vue";
import GridItemContent from "~/components/generic/grids/grid-item-content.vue";

export default {
    name: "SplitContentCard",
    data() {
      return {
        hover: false
      };
    },
    props: {
      content: {
        type: Object,
        required: true
      },
      //in this instance we share aspect ratio for both images, either from an item or by the grid component choices
      aspect: {
        type: String,
        required: true
      }
    },
    components: {
        StandardImageDisplay,
        GridItemContent
    },
    computed: {
      attributeType() {
        if (this.content.image.url) {
          return "a";
        } else return "div"
      },
      attributeClass() {
        if (this.content.image.url) {
          return "image-link";
        } else return "image-display"
      },
      targetNewWindow() {
        if (this.content.image.urlNewWindow != null && this.content.image.urlNewWindow) {
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
      }
    }
}
</script>

<style lang="scss" scoped>

.content-card{
  display:flex;
  flex-direction: column;
}

//setup image region for both images within hover state
//grid serves as replacement for absolute positioning

.content-card {
  .image-container {

    ::v-deep .object-contain {
        padding:1.5em;
    }
    .title-region {
      bottom:0;
      position: absolute;
      z-index:10;
      width:100%;
      display:flex;
      justify-content: center;
      padding:1em;
    }
    .title {
      margin:0;
      color:#fff;
    }
  }
}
 .content-card {
  display:grid;
  gap:1em;
  ::v-deep .banner-display{
  --main-banner-content-text-color: black;
  --banner-content-inner-padding: 0;
  --main-banner-title: 1.25em;
  --banner-content-inner-width:100%;
  }
}


.content-card-image-region {
    display:grid;
    position: relative;
}
.content-card-image-region > *{
    display: flex;
    grid-area: 1/1;
}
//z-indexing for hover image
.layer-1 {
    z-index:1;
}
.layer-2 {
    z-index:2;
}
/* transition for hover */

.fade-enter-active,
.fade-leave-active {
  transition: opacity .3s ease-in-out;
}

.fade-enter,
.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
</style>