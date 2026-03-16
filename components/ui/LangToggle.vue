<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted } from 'vue'

interface Language {
  code: string
  name: string
  flag: string
}

const props = withDefaults(defineProps<{
  /** 1 = Outlined Pill · 2 = Globe Accent · 3 = Flag Forward */
  variant?: 1 | 2 | 3
  /** Mirror the nav's scrolled state so trigger styles update */
  scrolled?: boolean
  modelValue?: string
}>(), {
  variant: 1,
  scrolled: false,
  modelValue: 'EN',
})

const emit = defineEmits<{
  'update:modelValue': [code: string]
}>()

const languages: Language[] = [
  { code: 'EN', name: 'English', flag: '🇬🇧' },
  { code: 'DE', name: 'Deutsch', flag: '🇩🇪' },
  { code: 'FR', name: 'Français', flag: '🇫🇷' },
  { code: 'ES', name: 'Español', flag: '🇪🇸' },
]

const isOpen = ref(false)
const rootRef = ref<HTMLElement | null>(null)

const current = computed(() =>
  languages.find(l => l.code === props.modelValue) ?? languages[0]
)

function select(code: string) {
  emit('update:modelValue', code)
  isOpen.value = false
}

function handleKeydown(e: KeyboardEvent) {
  if (e.key === 'Escape') isOpen.value = false
}

function handleOutsideClick(e: MouseEvent) {
  if (!rootRef.value?.contains(e.target as Node)) {
    isOpen.value = false
  }
}

onMounted(() => {
  document.addEventListener('click', handleOutsideClick)
  document.addEventListener('keydown', handleKeydown)
})

onUnmounted(() => {
  document.removeEventListener('click', handleOutsideClick)
  document.removeEventListener('keydown', handleKeydown)
})
</script>

<template>
  <div
    ref="rootRef"
    :class="['lt', `v${variant}`, { scrolled, open: isOpen }]"
  >

    <!-- ─── Trigger ─────────────────────────────────── -->
    <button
      class="lt-trigger"
      :aria-expanded="isOpen"
      aria-haspopup="listbox"
      aria-label="Select language"
      @click.stop="isOpen = !isOpen"
    >
      <!-- V1: Flag · Sep · Code -->
      <template v-if="variant === 1">
        <span class="lt-flag" aria-hidden="true">{{ current.flag }}</span>
        <span class="lt-sep" aria-hidden="true" />
        <span class="lt-code">{{ current.code }}</span>
      </template>

      <!-- V2: Globe icon · Code -->
      <template v-else-if="variant === 2">
        <svg class="lt-globe" viewBox="0 0 24 24" fill="none" stroke="currentColor" aria-hidden="true">
          <circle cx="12" cy="12" r="10" stroke-width="1.75" />
          <line x1="2" y1="12" x2="22" y2="12" stroke-width="1.5" />
          <path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z" stroke-width="1.5" />
        </svg>
        <span class="lt-code">{{ current.code }}</span>
      </template>

      <!-- V3: Flag · Full name (desktop) / Code (mobile) -->
      <template v-else>
        <span class="lt-flag" aria-hidden="true">{{ current.flag }}</span>
        <span class="lt-fullname">{{ current.name }}</span>
        <span class="lt-mobile-code" aria-hidden="true">{{ current.code }}</span>
      </template>

      <svg class="lt-chevron" viewBox="0 0 24 24" fill="none" stroke="currentColor" aria-hidden="true">
        <polyline points="6 9 12 15 18 9" />
      </svg>
    </button>

    <!-- ─── Panel ──────────────────────────────────── -->
    <div class="lt-panel" role="listbox" aria-label="Language options">

      <!-- V2 only: panel header -->
      <div v-if="variant === 2" class="lt-panel-header">
        <span class="lt-panel-label">Language</span>
      </div>

      <button
        v-for="lang in languages"
        :key="lang.code"
        :class="['lt-option', { active: modelValue === lang.code }]"
        role="option"
        :aria-selected="modelValue === lang.code"
        @click="select(lang.code)"
      >
        <span class="lt-opt-flag" aria-hidden="true">{{ lang.flag }}</span>
        <span class="lt-opt-code">{{ lang.code }}</span>
        <span class="lt-opt-name">{{ lang.name }}</span>
        <svg v-if="modelValue === lang.code" class="lt-check" viewBox="0 0 24 24" aria-hidden="true">
          <polyline points="20 6 9 17 4 12" />
        </svg>
      </button>

    </div>
  </div>
</template>

<style scoped>
/* ─── Shared base ───────────────────────────────────────── */
.lt { position: relative; }

.lt-trigger {
  font-family: var(--fs);
  cursor: pointer;
  line-height: 1;
  display: inline-flex;
  align-items: center;
}

/* Chevron */
.lt-chevron {
  width: 11px;
  height: 11px;
  stroke-width: 2.5;
  stroke-linecap: round;
  stroke-linejoin: round;
  flex-shrink: 0;
  transition: transform 200ms var(--ease);
}
.lt.open .lt-chevron { transform: rotate(180deg); }

/* Panel — shared base */
.lt-panel {
  position: absolute;
  top: calc(100% + 8px);
  right: 0;
  background: var(--white);
  z-index: 20;
  opacity: 0;
  visibility: hidden;
  transform: translateY(-5px) scale(0.98);
  transform-origin: top right;
  transition:
    opacity 200ms var(--ease),
    transform 200ms var(--ease),
    visibility 200ms;
}
.lt.open .lt-panel {
  opacity: 1;
  visibility: visible;
  transform: translateY(0) scale(1);
}

/* Check mark — shared */
.lt-check {
  fill: none;
  stroke: var(--sangria);
  stroke-width: 2.5;
  stroke-linecap: round;
  stroke-linejoin: round;
  flex-shrink: 0;
  margin-left: auto;
  width: 13px;
  height: 13px;
}


/* ─── V1 — Outlined Pill ────────────────────────────────── */
/*
   Trigger mirrors the "Back to homepage" outline button exactly:
   same 1.5px border, 6px radius, 38px height, 13px/600 Hanken.
   — unscrolled: white semi-transparent border + text
   — scrolled: solid sangria border; fills on hover
*/
.lt.v1 .lt-trigger {
  gap: 6px;
  font-size: 13px;
  font-weight: 600;
  padding: 8px 14px;
  border-radius: var(--rmd);
  min-height: 38px;
  border: 1.5px solid;
  background: transparent;
  letter-spacing: 0.01em;
  transition: all 200ms var(--ease);
}
.lt.v1:not(.scrolled) .lt-trigger {
  color: var(--white);
  border-color: rgba(255, 255, 255, 0.35);
}
.lt.v1:not(.scrolled) .lt-trigger:hover {
  background: rgba(255, 255, 255, 0.1);
  border-color: rgba(255, 255, 255, 0.55);
}
.lt.v1.scrolled .lt-trigger {
  color: var(--sangria);
  border-color: var(--sangria);
}
.lt.v1.scrolled .lt-trigger:hover {
  background: var(--sangria);
  color: var(--white);
  transform: translateY(-1px);
}

.lt.v1 .lt-flag { font-size: 15px; line-height: 1; }
.lt.v1 .lt-sep  { width: 1px; height: 11px; background: currentColor; opacity: 0.25; }
.lt.v1 .lt-code { font-size: 13px; font-weight: 700; letter-spacing: 0.05em; }

.lt.v1 .lt-panel {
  min-width: 168px;
  border-radius: var(--rlg);
  box-shadow: var(--sh-md), 0 0 0 1px rgba(0, 0, 0, 0.04);
  padding: 5px;
}
.lt.v1 .lt-option {
  display: flex;
  align-items: center;
  gap: 8px;
  width: 100%;
  padding: 8px 10px;
  border-radius: var(--rmd);
  border: none;
  background: none;
  font-family: var(--fs);
  color: var(--gd);
  cursor: pointer;
  text-align: left;
  transition: background 200ms var(--ease), color 200ms var(--ease);
}
.lt.v1 .lt-option:hover       { background: var(--gl); color: var(--sangria); }
.lt.v1 .lt-option.active      { color: var(--sangria); background: rgba(84, 23, 54, 0.05); }

.lt.v1 .lt-opt-flag { font-size: 15px; line-height: 1; flex-shrink: 0; }
.lt.v1 .lt-opt-code { font-size: 12px; font-weight: 700; letter-spacing: 0.05em; min-width: 22px; }
.lt.v1 .lt-opt-name { flex: 1; font-size: 12px; color: var(--gm); }
.lt.v1 .lt-option.active .lt-opt-name { color: rgba(84, 23, 54, 0.5); }


/* ─── V2 — Globe Accent ──────────────────────────────────── */
/*
   Trigger is ghost — globe icon signals "language" visually.
   A subtle border appears on hover/focus only.
   Panel is more elevated: has a "Language" header label and
   active rows get a 3px sangria left-accent bar for editorial feel.
*/
.lt.v2 .lt-trigger {
  gap: 5px;
  font-size: 13px;
  font-weight: 500;
  padding: 7px 10px;
  border-radius: var(--rmd);
  min-height: 36px;
  border: 1px solid transparent;
  background: none;
  letter-spacing: 0.04em;
  transition: all 200ms var(--ease);
}
.lt.v2:not(.scrolled) .lt-trigger         { color: rgba(255, 255, 255, 0.7); }
.lt.v2:not(.scrolled) .lt-trigger:hover   {
  color: var(--white);
  background: rgba(255, 255, 255, 0.08);
  border-color: rgba(255, 255, 255, 0.2);
}
.lt.v2.scrolled .lt-trigger               { color: var(--gm); }
.lt.v2.scrolled .lt-trigger:hover         {
  color: var(--sangria);
  background: rgba(84, 23, 54, 0.04);
  border-color: rgba(84, 23, 54, 0.15);
}

.lt.v2 .lt-globe {
  width: 15px;
  height: 15px;
  stroke-linecap: round;
  stroke-linejoin: round;
  flex-shrink: 0;
}
.lt.v2 .lt-code { font-size: 13px; font-weight: 600; letter-spacing: 0.06em; }

.lt.v2 .lt-panel {
  min-width: 210px;
  border-radius: 12px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12), 0 0 0 1px rgba(0, 0, 0, 0.04);
  padding: 0;
  overflow: hidden;
}
.lt.v2 .lt-panel-header {
  display: flex;
  align-items: center;
  padding: 11px 16px 9px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.06);
}
.lt.v2 .lt-panel-label {
  font-family: var(--fs);
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--gm);
}
.lt.v2 .lt-option {
  display: flex;
  align-items: center;
  gap: 11px;
  width: 100%;
  padding: 11px 16px;
  border: none;
  border-left: 3px solid transparent;
  background: none;
  font-family: var(--fs);
  font-size: 13px;
  color: var(--gd);
  cursor: pointer;
  text-align: left;
  transition:
    background 200ms var(--ease),
    color 200ms var(--ease),
    border-left-color 200ms var(--ease);
}
.lt.v2 .lt-option:not(:last-child) { border-bottom: 1px solid rgba(0, 0, 0, 0.045); }
.lt.v2 .lt-option:hover {
  background: var(--gl);
  color: var(--sangria);
  border-left-color: rgba(84, 23, 54, 0.3);
}
.lt.v2 .lt-option.active {
  color: var(--sangria);
  border-left-color: var(--sangria);
  background: rgba(84, 23, 54, 0.03);
}

.lt.v2 .lt-opt-flag { font-size: 18px; line-height: 1; flex-shrink: 0; }
.lt.v2 .lt-opt-code { display: none; } /* suppressed — name alone is cleaner here */
.lt.v2 .lt-opt-name { flex: 1; font-size: 13px; font-weight: 400; }
.lt.v2 .lt-option.active .lt-opt-name { font-weight: 600; }


/* ─── V3 — Flag Forward ──────────────────────────────────── */
/*
   Trigger shows the full language name beside the flag (desktop),
   collapses to code-only on mobile < 480px.
   Always has a subtle border — feels more like a "selector" widget
   than a ghost button. Active dropdown row gets a tinted sangria fill.
*/
.lt.v3 .lt-trigger {
  gap: 7px;
  font-size: 13px;
  font-weight: 500;
  padding: 8px 14px;
  border-radius: var(--rmd);
  min-height: 38px;
  border: 1.5px solid;
  cursor: pointer;
  letter-spacing: 0.01em;
  transition: all 200ms var(--ease);
}
.lt.v3:not(.scrolled) .lt-trigger {
  color: var(--white);
  border-color: rgba(255, 255, 255, 0.3);
  background: rgba(255, 255, 255, 0.08);
}
.lt.v3:not(.scrolled) .lt-trigger:hover {
  background: rgba(255, 255, 255, 0.15);
  border-color: rgba(255, 255, 255, 0.5);
}
.lt.v3.scrolled .lt-trigger {
  color: var(--gd);
  border-color: var(--g3);
  background: transparent;
}
.lt.v3.scrolled .lt-trigger:hover {
  border-color: var(--sangria);
  color: var(--sangria);
  background: rgba(84, 23, 54, 0.03);
}

.lt.v3 .lt-flag        { font-size: 17px; line-height: 1; }
.lt.v3 .lt-fullname    { font-size: 13px; font-weight: 500; white-space: nowrap; }
.lt.v3 .lt-mobile-code { display: none; font-size: 13px; font-weight: 600; letter-spacing: 0.04em; }

.lt.v3 .lt-panel {
  min-width: 210px;
  border-radius: 10px;
  box-shadow: var(--sh-md), 0 0 0 1px rgba(0, 0, 0, 0.05);
  padding: 5px;
}
.lt.v3 .lt-option {
  display: flex;
  align-items: center;
  gap: 10px;
  width: 100%;
  padding: 10px 12px;
  border-radius: 7px;
  border: none;
  background: none;
  font-family: var(--fs);
  color: var(--gd);
  cursor: pointer;
  text-align: left;
  transition: background 200ms var(--ease), color 200ms var(--ease);
}
.lt.v3 .lt-option:hover  { background: var(--gl); }
.lt.v3 .lt-option.active { background: rgba(84, 23, 54, 0.06); color: var(--sangria); }

.lt.v3 .lt-opt-flag { font-size: 20px; line-height: 1; flex-shrink: 0; }
.lt.v3 .lt-opt-code { font-size: 12px; font-weight: 700; letter-spacing: 0.05em; min-width: 24px; }
.lt.v3 .lt-option.active .lt-opt-code { color: var(--sangria); }
.lt.v3 .lt-opt-name { flex: 1; font-size: 12px; color: var(--gm); }
.lt.v3 .lt-option.active .lt-opt-name { color: rgba(84, 23, 54, 0.5); }


/* ─── Mobile ─────────────────────────────────────────────── */
@media (max-width: 480px) {
  /* V3 only: swap full name → short code */
  .lt.v3 .lt-fullname    { display: none; }
  .lt.v3 .lt-mobile-code { display: inline; }
}
</style>
