<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const currentLang = ref('EN')

function handleScroll() {
  isScrolled.value = window.scrollY > 80
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <nav :class="['blog-nav', { scrolled: isScrolled }]">
    <div class="blog-nav-inner">

      <NuxtLink to="/" class="blog-nav-logo">viatu</NuxtLink>

      <div class="blog-nav-right">

        <!--
          Language selector — change :variant to 1, 2, or 3 to preview each design:
          1 = Outlined Pill (matches Back button style)
          2 = Globe Accent  (elevated, editorial, with header label)
          3 = Flag Forward  (visual-first, shows full language name)
        -->
        <LangToggle v-model="currentLang" :scrolled="isScrolled" :variant="2" />

        <!-- Back to homepage -->
        <NuxtLink to="/" class="blog-back-btn">
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
            <polyline points="15 18 9 12 15 6" />
          </svg>
          <span class="blog-back-label">Back to homepage</span>
        </NuxtLink>

      </div>
    </div>
  </nav>
</template>

<style scoped>
/* ─── Shell ─────────────────────────────────────────── */
.blog-nav {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 100;
  transition: background 300ms var(--ease), box-shadow 300ms var(--ease);
}
.blog-nav.scrolled {
  background: rgba(255, 255, 255, 0.96);
  backdrop-filter: blur(16px);
  box-shadow: 0 1px 0 rgba(0, 0, 0, 0.06);
}
.blog-nav-inner {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
  height: 88px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

/* ─── Logo ───────────────────────────────────────────── */
.blog-nav-logo {
  font-family: var(--fp);
  font-size: 18px;
  letter-spacing: -0.04em;
  transition: color 300ms var(--ease);
}
.blog-nav:not(.scrolled) .blog-nav-logo { color: var(--white); }
.blog-nav.scrolled    .blog-nav-logo { color: var(--sangria); }

/* ─── Right cluster ──────────────────────────────────── */
.blog-nav-right {
  display: flex;
  align-items: center;
  gap: 10px;
}

/* ─── Back button ────────────────────────────────────── */
.blog-back-btn {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  font-family: var(--fs);
  font-size: 16px;
  font-weight: 700;
  line-height: 1.2;
  padding: 18px 20px;
  border-radius: 4px;
  letter-spacing: 0;
  white-space: nowrap;
  transition: all 200ms var(--ease);
}
.blog-nav:not(.scrolled) .blog-back-btn {
  color: var(--white);
  border: none;
  background: var(--sangria);
}
.blog-nav:not(.scrolled) .blog-back-btn:hover {
  background: #6b1d45;
  transform: translateY(-1px);
}
.blog-nav.scrolled .blog-back-btn {
  color: var(--white);
  border: none;
  background: var(--sangria);
}
.blog-nav.scrolled .blog-back-btn:hover {
  background: #6b1d45;
  transform: translateY(-1px);
}

/* ─── Mobile ─────────────────────────────────────────── */
@media (max-width: 480px) {
  .blog-back-label { display: none; }
  .blog-back-btn   { padding: 14px 14px; gap: 0; }
  .blog-nav-inner  { padding: 0 20px; }
}
</style>
