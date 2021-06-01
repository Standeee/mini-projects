<template>
  <section class="is-flex is-justify-content-center is-flex-wrap-wrap mt-6">
    <div v-for="article of multipleArticles" :key="article.slug" class="m-2">
      <NuxtLink :to="{ name: 'blog-slug', params: { slug: article.slug } }">
        <LazyBlogCard :article="article" class="card-resize" />
      </NuxtLink>
    </div>
  </section>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const articles = await $content('articles')
      .only(['title', 'description', 'img', 'slug', 'author', 'updatedAt'])
      .sortBy('createdAt', 'asc')
      .fetch()

    let multipleArticles = articles.concat(articles)
    multipleArticles = multipleArticles.concat(multipleArticles)

    return {
      articles,
      multipleArticles,
    }
  },
}
</script>

<style lang="scss">
.card-resize {
  max-width: 250px;
  min-height: 450px;
}
</style>
