<template>
  <div class="mt-12 grid gap-16 border-t-2 border-gray-100 pt-12">
    <div v-for="blog in blogPosts" :key="blog.id">
      <div>
        <nuxt-link to="/blog" class="inline-block">
          <span class="inline-flex items-center px-3 py-0.5 rounded-full text-sm font-medium leading-5 bg-indigo-100 text-indigo-800">
            Blog Post
          </span>
        </nuxt-link>
      </div>
      <nuxt-link :to="blog.path" class="block hover:bg-gray-100">
        <h3 class="mt-4 text-xl leading-7 font-semibold text-gray-900">
          {{ blog.title }}
        </h3>
        <p class="mt-3 text-base leading-6 text-gray-500">
          {{ blog.tldr }}
        </p>
      </nuxt-link>
      <div class="mt-6">
        <div class="flex text-sm leading-5 text-gray-500">
          <time>
            {{ longDate(blog.published) }}
          </time>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment'

  export default {
    layout: 'home',
    methods: {
      longDate(slugDate) {
        var a = moment(slugDate, "YYYY-MM-DD");
        return a.format("MMM Do, YYYY");
      }
    },
    async asyncData({ $content }){
      const blogPosts = await $content('blog').sortBy('published', 'desc').fetch()
      return { blogPosts }
    },
    
  }
</script>
