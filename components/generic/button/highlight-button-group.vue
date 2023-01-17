<template>
  <div class="text-block-actions" :class="moreThanOne(actions)" v-if="actions">
    <div
      v-for="(item, index) in actions"
      :key="index"
      class="text-block-action"
    >
      <highlight-button :title="item.linkTitle" :buttonType="item.buttonType" />
    </div>
  </div>
</template>

<script>
import highlightButton from "./highlight-button.vue";
export default {
  components: { highlightButton },
  methods: {
    moreThanOne(item) {
      if (Object.keys(item).length > 1) {
        return "actions";
      }
    },
  },
};
</script>

<style>
</style>