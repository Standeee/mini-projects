<template>
  <section class="section">
    <h1>{{ article.title }}</h1>
  </section>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const article = await $content('articles', params.slug).fetch()
    return { article }
  },
}
</script>
