<template>
  <main>
    <section class="page-title">
      <h1>Nuxt JAMStack Blog</h1>
    </section>
    <section class="blog-posts">
      <h2>Latest Articles</h2>
      <div v-for="post in posts" :key="post._id">
        <h3><a v-bind:href="post.slug.current" v-text="post.title" /></h3>
      </div>
    </section>
  </main>
</template>

<script>
import { groq } from '@nuxtjs/sanity'

export default {
  async asyncData({ $sanity }) {
    const query = groq`*[_type == "post"]`
    const posts = await $sanity.fetch(query)
    return { posts }
  }
}
</script>

<style>
  .main {
    margin: 2rem;
    min-height: 100vh;
  }
  .blog-posts {
    margin: 2rem 0;
  }
</style>
