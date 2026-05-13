<template>
  <div :class="{ rtl: isRtl }" :dir="isRtl ? 'rtl' : 'ltr'">
    <!-- Custom cursor -->
    <div class="cursor-dot" :style="{ left: cursor.x + 'px', top: cursor.y + 'px' }"></div>
    <div class="cursor-ring" :style="{ left: cursor.rx + 'px', top: cursor.ry + 'px' }"></div>

    <!-- Page transition -->
    <transition name="lang-fade">
      <div :key="lang" class="page-wrapper">
        <NavBar :d="d" :lang="lang" :isRtl="isRtl" :isDark="isDark" @toggleLang="toggleLang" @toggleTheme="toggleTheme" />
        <main>
          <HeroSection :d="d" :isRtl="isRtl" />
          <div class="divider container-divider"></div>
          <AboutSection :d="d" :isRtl="isRtl" />
          <div class="divider container-divider"></div>
          <ExperienceSection :d="d" :isRtl="isRtl" />
          <div class="divider container-divider"></div>
          <SkillsSection :d="d" :isRtl="isRtl" />
          <div class="divider container-divider"></div>
          <ProjectsSection :d="d" :isRtl="isRtl" />
          <div class="divider container-divider"></div>
          <ContactSection :d="d" :isRtl="isRtl" />
        </main>
        <FooterSection :d="d" :isRtl="isRtl" />
      </div>
    </transition>

    <!-- Back to top -->
    <transition name="fade">
      <button v-if="showTop" class="back-to-top" @click="scrollTop" :title="isRtl ? 'للأعلى' : 'Back to top'">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M12 19V5M5 12l7-7 7 7"/></svg>
      </button>
    </transition>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import { data } from './data/portfolio.js'
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import ExperienceSection from './components/ExperienceSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ContactSection from './components/ContactSection.vue'
import FooterSection from './components/FooterSection.vue'

const lang = ref('en')
const isRtl = computed(() => lang.value === 'ar')
const d = computed(() => data[lang.value])
const showTop = ref(false)
const isDark = ref(true)

function applyTheme(dark) {
  document.documentElement.setAttribute('data-theme', dark ? 'dark' : 'light')
  localStorage.setItem('theme', dark ? 'dark' : 'light')
}

function toggleTheme() {
  isDark.value = !isDark.value
  applyTheme(isDark.value)
}

// Custom cursor
const cursor = ref({ x: -100, y: -100, rx: -100, ry: -100 })
let ry = -100, rx = -100

function onMouseMove(e) {
  cursor.value.x = e.clientX
  cursor.value.y = e.clientY
}
function animateCursor() {
  rx += (cursor.value.x - rx) * 0.12
  ry += (cursor.value.y - ry) * 0.12
  cursor.value.rx = rx
  cursor.value.ry = ry
  requestAnimationFrame(animateCursor)
}

function toggleLang() {
  lang.value = lang.value === 'en' ? 'ar' : 'en'
  document.documentElement.lang = lang.value
  document.body.classList.toggle('rtl', lang.value === 'ar')
}

function scrollTop() { window.scrollTo({ top: 0, behavior: 'smooth' }) }

function onScroll() {
  showTop.value = window.scrollY > 500

  // Reveal animations
  document.querySelectorAll('.reveal, .reveal-left, .reveal-right').forEach(el => {
    const rect = el.getBoundingClientRect()
    if (rect.top < window.innerHeight - 80) {
      el.classList.add('visible')
    }
  })
}

onMounted(() => {
  // Restore saved theme
  const saved = localStorage.getItem('theme')
  if (saved === 'light') { isDark.value = false; applyTheme(false) }
  else { applyTheme(true) }

  window.addEventListener('mousemove', onMouseMove)
  window.addEventListener('scroll', onScroll)
  animateCursor()
  setTimeout(onScroll, 100)
})
onUnmounted(() => {
  window.removeEventListener('mousemove', onMouseMove)
  window.removeEventListener('scroll', onScroll)
})
</script>

<style>
/* ─── Custom Cursor ─── */
.cursor-dot {
  position: fixed;
  width: 8px;
  height: 8px;
  background: var(--accent-1);
  border-radius: 50%;
  pointer-events: none;
  z-index: 10000;
  transform: translate(-50%, -50%);
  transition: background 0.3s;
  mix-blend-mode: normal;
}
.cursor-ring {
  position: fixed;
  width: 36px;
  height: 36px;
  border: 1.5px solid rgba(108,99,255,0.5);
  border-radius: 50%;
  pointer-events: none;
  z-index: 9999;
  transform: translate(-50%, -50%);
}

/* ─── Page transition ─── */
.lang-fade-enter-active, .lang-fade-leave-active { transition: opacity 0.4s ease; }
.lang-fade-enter-from, .lang-fade-leave-to { opacity: 0; }

/* ─── Back to top ─── */
.back-to-top {
  position: fixed;
  bottom: 32px;
  right: 32px;
  width: 46px;
  height: 46px;
  border-radius: 50%;
  background: linear-gradient(135deg, var(--accent-1), #8b5cf6);
  color: #fff;
  border: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 20px rgba(108,99,255,0.4);
  transition: all 0.3s;
  z-index: 900;
}
.back-to-top:hover { transform: translateY(-4px); box-shadow: 0 8px 30px rgba(108,99,255,0.6); }

.fade-enter-active, .fade-leave-active { transition: opacity 0.3s; }
.fade-enter-from, .fade-leave-to { opacity: 0; }

.container-divider { max-width: 1100px; margin: 0 auto; padding: 0 24px; }
.container-divider .divider { margin: 0; }

/* RTL back-to-top */
.rtl .back-to-top { right: auto; left: 32px; }

@media (max-width: 768px) {
  .cursor-dot, .cursor-ring { display: none; }
}
</style>
