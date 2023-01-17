<template>
    <div class="content-page">

    <section  class="terms-conditions">
        <div class="content-container">
            <WysiwygContentDisplay :content="terms.content" :lineHeight="terms.lineHeight" class="text-intro text-block"/>
        </div>
    </section>
    </div>
</template>

<script>
import StandardImage from '~/components/generic/image/standard-image-display.vue'
import StandardImageParallaxDisplay from '~/components/generic/image/standard-image-parallax-display.vue'
import WysiwygContentDisplay from '~/components//wysiwyg-content-display.vue'
import StandardGrid from '~/components/generic/grids/standard-grid.vue'

export default {
  components: { 
    StandardImage,
    StandardImageParallaxDisplay,
    WysiwygContentDisplay,
    StandardGrid
  },
  data() {
    return {
        terms: {
            lineHeight: 'standard',
            content: "<h1>Terms and Conditions</h1><p>This competition is promoted by UNOVINO Pty Ltd whose registered offices are located at 13 Greenhill Road Wayville South Australia 5034.</p><p>UNOVINO Pty Ltd ABN 14659308282 South Australia Packaged Liquor Sales License 57711157.</p><p>This competition is only for Australian Residents 18 years and older, except for employees of UNOVINO Pty Ltd and their families and associated companies.</p><p>This promotion starts on 19 January 2023 and will at close on 24 March 2023 at 12 pm ACST with the winner notified by 28 March 2023 and results published on the UNOVINO website.</p><p>To enter the competition you must purchase a product from the UNOVINO website on or before 24 March 2023 and indicate your willingness to participate in the draw for one year\'s worth of wine. Each purchase from the UNOVINO website allows you to enter the draw. The competition's purpose is to act as a promotion for UNOVINO and the products available for purchase from the UNOVINO website.</p><p>The prize - one year of wine is defined as wine to the value of $2,200 selected from wineries and products displayed on the UNOVINO website. The prize may be taken as quarterly, six-monthly or single delivery. Note the minimum quantity of 6 bottles from an individual winery is required and selection is subject to stock availability at the time.</p><p>By entering this competition you are consenting to receive communication from UNOVINO Pty Ltd until such time as you request to opt out.</p><p>Your entry and personal details are covered by UNOVINO Privacy Policy which is available on UNOVINO's website. Your details will not be sold or rented to any other companies.</p><p>The winner will be drawn at random.</p><p>There will be no cash alternatives for the prize offered.</p>"
        }
    };
  }
}

</script>
