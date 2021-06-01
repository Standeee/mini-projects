<template>
  <div class="card">
    <div class="card-image">
      <figure class="image is-4by3">
        <img
          src="https://bulma.io/images/placeholders/1280x960.png"
          alt="Placeholder image"
        />
      </figure>
    </div>
    <div class="card-content">
      <div class="media">
        <div class="media-left">
          <figure class="image is-48x48">
            <img
              src="https://bulma.io/images/placeholders/96x96.png"
              alt="Placeholder image"
            />
          </figure>
        </div>
        <div class="media-content">
          <p class="title is-6">{{ article.author.name }}</p>
          <p class="subtitle is-6">{{ article.author.username }}</p>
        </div>
      </div>

      <div
        class="
          content
          is-flex is-flex-direction-column is-justify-content-space-between
        "
      >
        <p>{{ article.title }}<br /></p>
        <time datetime="2016-1-1"
          ><b-icon icon="clock-time-three-outline" size="is-small"> </b-icon>
          {{ formatDate }}</time
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    article: {
      type: Object,
      default: null,
      required: true,
    },
  },
  computed: {
    formatDate() {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(this.article.updatedAt).toLocaleDateString('en', options)
    },
  },
}
</script>

<style lang="scss">
.content {
  height: 140px;
}
</style>
