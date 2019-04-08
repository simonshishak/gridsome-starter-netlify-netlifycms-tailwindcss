<template>
  <Layout>
    <div class="mt-8">
      <h1 class="pb-1 text-xl font-bold">
        {{ $page.post.title }}
      </h1>
      <div class="my-4">
        Posted {{ $page.post.date }}
        <template v-if="$page.post.timeToRead">
          <strong>{{ $page.post.timeToRead }} min read.</strong>  
        </template>  
      </div>
    </div>
    <div class="post__header">
      <img alt="Cover image" class="w-full rounded rounded-b-none h-48 object-cover" v-if="$page.post.coverImage" :src="$page.post.coverImage" />
    </div>
    <div class="px-4 py-4 rounded shadow-lg">
      <div class="mt-8" v-html="$page.post.content" />
    </div>
    <div class="py-4">
      <div class="post-tags">
        <g-link v-for="tag in $page.post.tags" :key="tag.id" :to="tag.path">
          <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2">#{{ tag }}</span>
        </g-link>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query Post($path: String!) {
  post: post(path: $path) {
    title
    path
    date (format: "MMM D YYYY")
    timeToRead
    tags
    content
    coverImage (height: 320, quality: 100)
  }
}
</page-query>

<script>
export default {}
</script>

<style lang="scss">
</style>