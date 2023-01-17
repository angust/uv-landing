<template>
    <div class="content-page">

    <section  class="terms-conditions">
        <div class="content-container">
            <WysiwygContentDisplay :content="privacy.content" :lineHeight="privacy.lineHeight" class="text-intro text-block"/>
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
        privacy: {
            lineHeight: 'standard',
            content: "<h1>Unovino Privacy Policy</h1><h5>Revision Date: 04 September 2022.</h5><p>Unovino Pty Ltd (ACN 659 308 282) (Unovino, we, us and our) is committed to compliance with Australia\'s National Privacy Principles (NPPs) and this Privacy Policy explains the approach to dealing with your personal information.&nbsp;</p><p>The policy applies only to the Unovino website, marketplace and platform (<a href=\"http://www.unovino.com\" rel=\"noopener noreferrer\" target=\"_blank\">www.unovino.com</a>) and applies to all ‘personal information’ we hold. ‘Personal information’ is defined as any information that identifies or can be used to identify the person to whom such information pertains. The security of your personal information is very important to us, and this policy details how data about you is used when you access our website and services or interact with us.&nbsp;&nbsp;</p><p>This policy also applies to personal information that we have obtained from third parties such as the providers of Goods or Services we market through this site.</p><h3>Your Consent</h3><p>By using the Unovino site you consent to Unovino maintaining, recording, holding and using the personal information we collect about you that will be subject to this Privacy Policy which will be as amended from time to time.&nbsp;</p><p>This Privacy Policy does not govern privacy practices associated with offline activities, or websites other than the Unovino website.</p><h3>Policy Updates</h3><p>We may, from time to time, review and update this privacy policy, including taking into account new or amended laws, new technology and/or changes to our operations. All personal information held by us will be governed by the most recently updated policy.</p><p>Please regularly review this policy and if we update it, we will revise the Revision Date above.</p><p>If as the result of any such changes you have objections to the Privacy Policy, you should immediately discontinue use of the Unovino site and contact us to update your personal information and privacy preferences.</p>"
        }
    };
  }
}

</script>
