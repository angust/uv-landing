<template>
  <div id="web-form" class="competition-form">
<!--     <div class="web-form-background">
      <img src="/assets/banner/vineyard.jpg" class="web-form-background-image" />
    </div> -->

    <div
      class="typeform-widget"
      :data-url="typeformUrl"
      style="width: 100%; height: 600px;"
      data-hide-headers="true"
      data-hide-footer="true"
    ></div>
  </div>
</template>

<script>
//a component to display typefrom webform, requires a typeform link to be passed in a prop
export default {
  name: "WebForm",
  props: {
    typeformUrl: {
      type: String,
      required: true
    },
  },
  mounted() {
    var qs,
      js,
      q,
      s,
      d = document,
      gi = d.getElementById,
      ce = d.createElement,
      gt = d.getElementsByTagName,
      id = "typef_orm",
      b = "https://embed.typeform.com/";

    if (!gi.call(d, id)) {
      js = ce.call(d, "script");
      js.id = id;
      js.src = b + "embed.js";
      q = gt.call(d, "script")[0];
      q.parentNode.insertBefore(js, q);
    }
  }
};
</script>

<style lang="scss" scoped>
//data-transparency="100"
.web-form-form {
  position: relative;
  overflow: hidden;
}
.web-form-background {
  position: absolute;
  height: 100%;
  width: 100%;
  z-index: 0;

/*   &:before {
    background: linear-gradient(
      180deg,
      var(--main-background-color),
      rgba(255, 255, 255, 0)
    );
    height: 100%;
    width: 100%;
    position: absolute;
    top: 0;
    content: " ";
    z-index: 1;
  } */
}
.web-form-background-image {
  object-fit: cover;
  width: 100%;
  height: 100%;
  position: absolute;
  left: 0;
  top: 0;
  opacity: 0.6;
  @include media-breakpoint-up(md) {
    opacity: 0.75;
  }
}
</style>