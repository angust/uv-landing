<template>
  <div class="page">
  <standard-image-parallax-display 
    source="/images/banners/home-banner-1.jpg" 
    aspect="fluid"
    object-position="top"
    object-fit="cover"
    class="main-banner"
    alt="Banner"
  >
    <div slot="image-content-layer" class="banner-content-layer">
        <div class="content-container">
          <div class="content-text">
            <LogoWhite />
            </div>
        </div>
      </div>
  </standard-image-parallax-display>

  <section>
    <div class="content-container">
        <WysiwygContentDisplay :content="intro.content" :lineHeight="intro.lineHeight" class="text-intro text-block"/>
    </div>
  </section>

  <section>
    <TypeformElement typeform-url="https://z6pnfa6mlc1.typeform.com/to/iwCsBSbz" />
  </section>

  <section  class="terms-conditions">
    <div class="content-container">
        <WysiwygContentDisplay :content="terms.content" :lineHeight="terms.lineHeight" class="text-intro text-block"/>
    </div>
  </section>

<!--   <section>
  <div class="content-container">
    <Partners />
  </div>
  </section> -->

<!-- 
  <section class="difference-set">
    <div class="content-container">

      <standard-grid
        :gridGap="difference.gridGap"
        :gridColumns="difference.gridColumns"
        :items="difference.items"
      >
        <template v-slot:item="{ item, key }">
          <SplitContentCard :content="item" :aspect="difference.imageAspectRatio" />
        </template>
  </standard-grid>
  
    </div>
  </section>

  <section>
  <div class="content-container">
    <div class="content-grid grid-50-50">
   <div class="image-block">
 
    <div class="ratio-block">
      <standard-image 
        source="/images/cta/square-image-1.jpg" 
        aspect="1-1"
        object-position="center"
        object-fit="cover"
        class="ratio-block-item"
        style="--ratio: 1 / 1;"
      />
      <standard-image 
        source="/images/cta/3-4-image-1.jpg" 
        aspect="3-4"
        object-position="center"
        object-fit="cover"
        class="ratio-block-item"
        style="--ratio: 3 / 4;"
      />
      </div>
    
    </div>
    <WysiwygContentDisplay :content="second.content" :lineHeight="second.lineHeight" class="text-block"/>
  
    </div>
  </div>
  </section>
  <section>
  <div class="content-container">
    <div class="content-grid grid-50-50">

    <WysiwygContentDisplay :content="third.content" :lineHeight="third.lineHeight" class="text-block"/>
   <div class="image-block">
      <standard-image 
        source="/images/cta/3-4-image-1.jpg" 
        aspect="3-4"
        object-position="center"
        object-fit="cover"
      />
    </div>
    </div>
  </div>
  </section>
 -->

  </div>
</template>

<script>
import StandardImage from '~/components/generic/image/standard-image-display.vue'
import StandardImageParallaxDisplay from '~/components/generic/image/standard-image-parallax-display.vue'
import WysiwygContentDisplay from '~/components//wysiwyg-content-display.vue'
import StandardGrid from '~/components/generic/grids/standard-grid.vue'
import SplitContentCard from "~/components/generic/grids/split-content-card.vue";
import Partners from "~/components/partners.vue";
import TypeformElement from '~/components/forms/typeform-element.vue';

export default {
  components: { 
    StandardImage,
    StandardImageParallaxDisplay,
    WysiwygContentDisplay,
    StandardGrid,
    SplitContentCard,
    Partners,
    TypeformElement
  },
  data() {
    return {

      terms:  {
        content: "PACKAGED LIQUOR SALES LICENCE 57711157 </br> The competition runs from 12:01am ACST on the 19th Janurary 2023 and will close on 24th March 2023 at 11:59pm ACST.  The winner will be drawn at random and will be notified and published here.  For full competition T's and C's and our privacy policy please click on the link below: <a href='terms-conditions' class='highlight'>Terms & Conditions</a> <a href='privacy-policy' class='highlight'>Privacy Policy</a>",
        lineHeight: 'standard'
      },
      difference: {
        gridGap: 2,
        gridColumns: {
          small: 1,
          medium: 1,
          large: 3,
        },
        imageAspectRatio: "1-1",
        items: [
                {
          text: {
            BannerTextAlignment: "banner-text-center",
              title: "Buy from Artisans not warehouses",
              description: "We’re a platform for independent producers, so you know who you're buying from and what they stand for every time.",
              actions: [
                  {
                      "buttonSize": "standard",
                      "buttonType": "square",
                      "buttonStyle": "solid",
                      "linkUrl": "https://google.com/",
                      "linkTitle": null
                  }
              ]
          },
          image: {
            filepath: "https://images.unsplash.com/photo-1612163829979-f8aaf4f12b11?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=800&q=80",
            alt: "Red Wine",
            title: "Red Wine",
            objectPosition: "center",
            objectFit: "cover",
            tint:0,
            url: "https://www.elbournewines.com.au/",
            urlNewWindow: true
          },
          imageHover: {
            filepath: "https://images.unsplash.com/photo-1548957538-84e1176070d5?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=987&q=80",
            alt: "Elbourne Wines",
            title: "Elbourne Wines",
            objectPosition: "top",
            objectFit: "contain",
            tint:10,
          },
        },
        {
          text: {
              
            BannerTextAlignment: "banner-text-center",
              title: "No middlemen involved",
              description: "Wineries send your order directly to you, at home or pickup spot. No markups from distributors or conglomerates.",
              actions: []
          },
          image: {
            filepath: "https://images.unsplash.com/photo-1570598912132-0ba1dc952b7d?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=987&q=80",
            objectFit:"contain",
            alt: "Bleasdale Logo",
            title:  "Bleasdale Logo",
            objectPosition: "bottom",
            objectFit:"cover",
            tint:0,
            url: "https://www.bleasdale.com.au/",
            urlNewWindow: false
          },
          imageHover: {
            filepath: "https://images.unsplash.com/photo-1560512823-829485b8bf24?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=987&q=80",
            objectFit:"contain",
            alt: "Bleasdale wines display",
            title:  "Bleasdale wines display",
            objectPosition: "center",
            objectFit:"contain",
            tint:0
          },
        },
        {
          text: {
              BannerTextAlignment: "banner-text-center",
              title: "Better for everyone",
              description: "You receive uniquely crafted, limited-production wines, and learn the stories of the people you're supporting behind the bottle.",
              actions: [
                  {
                      "buttonSize": "standard",
                      "buttonType": "square",
                      "buttonStyle": "solid",
                      "linkUrl": "https://google.com/",
                      "linkTitle": null
                  }
              ]
          },
          image: {
            filepath: "https://images.unsplash.com/photo-1534003579377-e30914c1d25c?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1200&q=80",
            objectFit:"contain",
            alt: "Dowie Doole",
            title: "Dowie Doole",
            objectPosition: "center",
            objectFit:"cover",
            tint:0
          },
          imageHover: {
            filepath: "https://images.unsplash.com/photo-1616186793090-b49b8ca005e8?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1364&q=80",
            objectFit:"contain",
            alt: "Dowie Doole cellar door",
            title: "Dowie Doole cellar door",
            objectPosition: "center",
            objectFit:"cover",
            tint:0
          },
        }
        ]
      },
      introGrid: {
        gridGap: 2,
        gridColumns: {
          small: 1,
          medium: 2,
          large: 3,
        },
      },      
      intro:{
          lineHeight: 'spaced',
          content: "<h2>The most sophisticated <span class='highlight'>DTC Community Platform</span> connecting Iconic Wine Brands to Premium Wine Buyers so they can enjoy Cellar Door Only wines anytime, anywhere!</h2>",
      },
      second:{
          lineHeight: 'standard',
          content: "<h2>We believe Australian wineries deserve better.</h2><p>We partner with small aussie producers to bring you a diverse offering of wines that you wouldn't find in high volume stores.</p><p>You'll also learn more about the people behind the labels, from minority-owned winemakers who specialize in single-vineyard rieslings to veteran-owned winemakers producing some of the highest rated wines throughout Australia.</p>",
      },
      third: {
          lineHeight: 'standard',
          content: "<h2>We help you buy directly from boutique wineries with amazing wines.</h2><p>We help wineries share their stories with an audience of passionate wine drinkers (aka you!), and help people like you discover awesome one-of-a kind wineries, all in one place. At the heart of our business model is our mission.</p>"
      }
    };
  }
}
</script>


<style lang="scss" scoped>

section.terms-conditions{
  color: #99acd2;
}
::v-deep .difference-set {
  .content-card {
    .banner-display {
      --main-banner-content-text-color: white !important;
      --main-banner-title: 1.45em;
      --main-banner-description-font-size:1.1em;
    }
  }
}
.text-intro  {
    max-width: 820px;
    text-align: center;
    margin: 0 auto;
}

.main-banner {
  .content-text {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
      > * + * {
      margin-top: 2rem;
     }
     .description {
      font-size: 1.2em;
     }
  }
 :deep(.banner-content-layer) {
    position: absolute;
    bottom: 0;
    z-index: 2;
    display: flex;
    align-items: flex-end;
    justify-content: center;
    width: 100%;
    background: linear-gradient(360deg, #010032, transparent);
    padding-bottom: 5em;
    color: white;
    height: 100%;
  }
:deep(.image-container) {
position: relative;
}
:deep(.image-inner) {
    min-height:40em;
  }
}

section {
  padding:3em 0em;
  background:#010032;
  color:#fff;
}

.content-grid {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-gap: 2em;

  &.grid-50-50 {
    grid-gap: 1em;
    grid-row-gap: 5em;
    @include media-breakpoint-up(lg) {
      grid-gap: 5em;
    }
    .text-block,
    .image-block {
      grid-column: span 12;
    }
    @include media-breakpoint-up(lg) {
      .text-block,
      .image-block {
        grid-column: span 6;
      }
    }
  }
  &.grid-70-30 {
    grid-gap: 1em;
    grid-row-gap: 5em;
    @include media-breakpoint-up(lg) {
      grid-gap: 5em;
    }
    .text-block,
    .image-block {
      grid-column: span 12;
    }
    @include media-breakpoint-up(lg) {
      .text-block{
        grid-column: span 8;
      }
      .image-block {
        grid-column: span 4;
      }
    }
  }
  &.grid-60-40 {
    grid-gap: 1em;
    grid-row-gap: 5em;
    @include media-breakpoint-up(lg) {
      grid-gap: 5em;
    }
    .text-block,
    .image-block {
      grid-column: span 12;
    }
    @include media-breakpoint-up(lg) {
      .text-block{
        grid-column: span 8;
      }
      .image-block {
        grid-column: span 4;
      }
    }
  }
  .text-block {
    grid-column: span 5;
  }

  .image-block {
    grid-column: span 7;
  }
}


.ratio-block  {
    display: flex;
    grid-gap: 1rem;
    gap: 1rem;
    --modifier-width: 768px;
    --modifier: calc((var(--modifier-width) - 100%) * 999);
}
.ratio-block-item {
    flex-basis: max(var(--modifier), 0px);
    flex-grow: calc(var(--ratio));
    aspect-ratio: var(--ratio);
}

</style>