<script setup lang="ts">
definePageMeta({ layout: 'blog' })

const slug = useRoute().params.slug as string
// e.g. /author/lena-schmidt
</script>

<template>
  <!-- Author profile page
       Routes: /author/lena-schmidt
               /author/barbara-rodrigues
       See design/mockups/blog-author-v1.html for visual reference
  -->
  <div>
    <!-- TODO: AuthorHero — full-bleed background, large portrait, name + role + bio + stats -->
    <!-- TODO: AuthorArticleGrid — 3-col grid of ArticleCard, filtered by this author -->
    <!-- TODO: TagPagination -->
  </div>
</template>
