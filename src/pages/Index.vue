<template>
  <Layout>
    <Pager :info="$page.posts.pageInfo" />
    <div v-for="post in $page.posts.edges" :key="post.id" class="max-w rounded overflow-hidden shadow-lg mt-8">
      <img :src="post.node.coverImage" class="w-full h-48 object-cover"/>
      <div class="px-6 py-4">
        <div class="font-bold text-xl mb-2">{{post.node.title}}</div>
        <p class="text-gray-700 text-base">
          {{post.node.excerpt}}
        </p>
        <g-link :to="post.node.path">Read more...</g-link>
      </div>
      <div class="px-6 py-4">
        <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2">#photography</span>
        <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2">#travel</span>
        <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700">#winter</span>
      </div>
    </div>
  </Layout>
</template>

<page-query>
  query Home ($page: Int) {
    posts: allPost (perPage: 10, page: $page) @paginate {
      pageInfo {
        totalPages
        currentPage
      }
      edges {
        node {
          _id
          title
          path
          excerpt
          coverImage (height: 320, quality: 100)
        }
      }
    }
  }
</page-query>

<script>
import { Pager } from 'gridsome'
export default {
  components: {
    Pager
  }
}
</script>

<style>
.home-links a {
  margin-right: 1rem;
}
</style>
