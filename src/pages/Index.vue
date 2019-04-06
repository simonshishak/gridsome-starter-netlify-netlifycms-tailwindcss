<template>
  <Layout>
    <Pager :info="$page.allPost.pageInfo" />
    <div v-for="{ node } in $page.allPost.edges" :key="node.id" class="max-w rounded overflow-hidden shadow-lg mt-8">
      <g-image class="w-full" :src="node.coverImage" alt="Sunset in the mountains"></g-image>
      <div class="px-6 py-4">
        <div class="font-bold text-xl mb-2">{{node.title}}</div>
        <p class="text-gray-700 text-base">
          {{node.excerpt}}
        </p>
        <g-link :to="node.path">Read more...</g-link>
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
    allPost (perPage: 10, page: $page) @paginate {
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
          coverImage
        }
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
