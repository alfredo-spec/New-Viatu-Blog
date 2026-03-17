<script setup lang="ts">
definePageMeta({ layout: 'blog' })

// slug[0] = root tag (e.g. 'destinations')
// slug[1] = child tag (e.g. 'namibia')  — optional
const slug = useRoute().params.slug as string[]
const rootTag = computed(() => slug[0] ?? '')
const childTag = computed(() => slug[1] ?? null)
</script>

<template>
  <!-- Tag listing page
       Routes: /tag/destinations
               /tag/destinations/namibia
               /tag/experiences
               /tag/experiences/gorilla-trekking
       See design/mockups/blog-tag-listing-v1.html for visual reference
  -->
  <div>
    <!-- TODO: TagHero — shorter hero showing tag name + article count + breadcrumb -->
    <!-- TODO: BlogBrowseBar — active pill matches rootTag -->
    <!-- TODO: TagArticleGrid — 3-col grid of ArticleCard, filtered by tag -->
    <!-- TODO: TagPagination -->
  </div>
</template>
