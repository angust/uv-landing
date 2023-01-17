  <template>
  <div class="image-attribution">
    <div class="image-attribution-inner">
      <div class="description" v-if="authorDescription">
        {{ authorDescription }}
      </div>
      <div v-if="authorInfo" class="preposition">by</div>
      <div class="author" v-html="authorInfo" />
    </div>
  </div>
</template>

<script>
export default {
  name: "ContentImageInfo",
  props: {
    authorDescription: {
      type: String,
      required: false,
    },
    authorName: {
      type: String,
      required: false,
    },
    authorUrl: {
      type: String,
      required: false,
    },
  },
  computed: {
    //show name & link of author if available
    authorDisplay() {
      if (this.authorName) {
        return `${this.authorName}`;
      }
    },
    authorInfo(authorName, authorUrl, authorDisplay) {
      if (authorDisplay && this.authorUrl) {
        return `<a href="${this.authorUrl}" target="_blank" rel="noopener noreferrer">${this.authorDisplay}</a>`;
      } else if (this.authorDisplay || !this.authorUrl) {
        return this.authorDisplay;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.image-attribution-inner {
  word-break: break-word;

  .description {
    display: inline;
  }
  div {
    margin: 0;
    display: inline-block;
    &:first-of-type {
      &:first-letter {
        text-transform: uppercase;
      }
    }
  }
}
</style>