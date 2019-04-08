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
      <!-- <PostMeta :post="$page.post" /> -->

    </div>
    
    <div class="post content-box">
      <div class="post__header">
        <img alt="Cover image" class="w-full h-48 object-cover" v-if="$page.post.coverImage" :src="$page.post.coverImage" />
      </div>

      <div class="mt-8" v-html="$page.post.content" />

      <div class="post__footer">
        <!-- <PostTags :post="$page.post" /> -->
      </div>
    </div>

    <!-- <Author class="post-author" /> -->
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
.post-title {
  padding: calc(var(--space) / 2) 0 calc(var(--space) / 2);
  text-align: center;
}
.post {
  &__header {
    width: calc(100% + var(--space) * 2);
    margin-left: calc(var(--space) * -1);
    margin-top: calc(var(--space) * -1);
    margin-bottom: calc(var(--space) / 2);
    overflow: hidden;
    border-radius: var(--radius) var(--radius) 0 0;
    
    img {
      width: 100%;
    }
    &:empty {
      display: none;
    }
  }
  &__content {
    h2:first-child {
      margin-top: 0;
    }
    p:first-of-type {
      font-size: 1.2em;
      color: var(--title-color);
    }
    img {
      width: calc(100% + var(--space) * 2);
      margin-left: calc(var(--space) * -1);
      display: block;
      max-width: none;
    }
  }
}
.post-comments {
  padding: calc(var(--space) / 2);
  
  &:empty {
    display: none;
  }
}
.post-author {
  margin-top: calc(var(--space) / 2);
}
</style>