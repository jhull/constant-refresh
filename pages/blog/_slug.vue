<template>
<div class="relative py-16 bg-white overflow-hidden">
  <div class="relative px-4 sm:px-6 lg:px-8">
    <div class="text-lg max-w-prose mx-auto mb-6">
      <p class="text-base text-center leading-6 text-indigo-600 font-semibold tracking-wide uppercase">From the blog</p>
      <h1 class="mt-2 mb-8 text-3xl text-center leading-8 font-extrabold tracking-tight sm:text-4xl sm:leading-10">{{ post.title }}</h1>
      <p class="text-xl text-center leading-8">{{ post.tldr }}</p>
    </div>
    <div class="prose prose-lg mx-auto">
      <nuxt-content :document='post'/>
    </div>
  </div>
</div>
</template>

<script>
  export default {
    layout: 'blog',
    async asyncData ({ $content, params }) {
      const post = await $content('blog', params.slug).fetch()

      return {
        post
      }
    },
    head () {
      return {
        title: this.post.title + ' - Blog - constantRefresh',
      }
    }
    
  }
</script>