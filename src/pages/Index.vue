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
        <div class="mt-2">
          Posted {{ post.node.date }}
          <template v-if="post.node.timeToRead">
            <strong>{{ post.node.timeToRead }} min read.</strong>  
          </template>  
        </div>
      </div>
      <div class="px-6 py-4">
        <div class="post-tags">
          <g-link v-for="tag in post.node.tags" :key="tag.id" :to="tag.path">
            <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2">#{{ tag }}</span>
          </g-link>
        </div>
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
          date (format: "MMM Do YYYY")
          title
          path
          excerpt
          tags
          coverImage (height: 320, quality: 100)
          timeToRead
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
