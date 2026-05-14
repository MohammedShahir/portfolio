<template>
  <nav class="navbar" :class="{ scrolled: scrolled, rtl: isRtl }">
    <div class="nav-inner">
      <a href="#hero" class="nav-logo">
        <span class="logo-bracket">&lt;</span>
        <span class="logo-name">{{ d.name }}</span>
        <span class="logo-bracket"> /&gt;</span>
      </a>

      <div class="nav-links">
        <a
          v-for="(link, i) in d.navLinks"
          :key="i"
          :href="`#${d.navIds[i]}`"
          class="nav-link"
          :class="{ active: activeSection === d.navIds[i] }"
        >{{ link }}</a>
      </div>

      <div class="nav-actions">
        <!-- Theme Toggle -->
        <button class="theme-toggle" @click="$emit('toggleTheme')" :title="isDark ? (isRtl ? 'الوضع النهاري' : 'Light Mode') : (isRtl ? 'الوضع الليلي' : 'Dark Mode')">
          <transition name="icon-flip" mode="out-in">
            <span v-if="isDark" key="sun" class="theme-icon">☀️</span>
            <span v-else key="moon" class="theme-icon">🌙</span>
          </transition>
        </button>
        <!-- Language Toggle -->
        <button class="lang-toggle" @click="$emit('toggleLang')" :title="lang === 'en' ? 'العربية' : 'English'">
          <span class="lang-icon">🌐</span>
          <span>{{ lang === 'en' ? 'العربية' : 'English' }}</span>
        </button>
        <button class="hamburger" @click="menuOpen = !menuOpen" :class="{ open: menuOpen }">
          <span></span><span></span><span></span>
        </button>
      </div>
    </div>

    <!-- Mobile Menu -->
    <transition name="mobile-menu">
      <div v-if="menuOpen" class="mobile-menu">
        <a
          v-for="(link, i) in d.navLinks"
          :key="i"
          :href="`#${d.navIds[i]}`"
          class="mobile-link"
          @click="menuOpen = false"
        >{{ link }}</a>
      </div>
    </transition>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const props = defineProps({ d: Object, lang: String, isRtl: Boolean, isDark: Boolean })
defineEmits(['toggleLang', 'toggleTheme'])

const scrolled = ref(false)
const menuOpen = ref(false)
const activeSection = ref('hero')

function onScroll() {
  scrolled.value = window.scrollY > 50
  const sections = props.d.navIds
  for (const id of [...sections].reverse()) {
    const el = document.getElementById(id)
    if (el && window.scrollY >= el.offsetTop - 120) {
      activeSection.value = id
      break
    }
  }
}

onMounted(() => window.addEventListener('scroll', onScroll))
onUnmounted(() => window.removeEventListener('scroll', onScroll))
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 999;
  padding: 20px 0;
  transition: all 0.4s ease;
}
.navbar.scrolled {
  background: rgba(5,5,16,0.85);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(255,255,255,0.06);
  padding: 12px 0;
}
.nav-inner {
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 24px;
  display: grid;
  grid-template-columns: auto 1fr auto;
  grid-template-areas: 'logo links actions';
  align-items: center;
  gap: 16px;
}
.nav-logo {
  grid-area: logo;
  font-size: 1.1rem;
  font-weight: 700;
  text-decoration: none;
  color: var(--text-primary);
  white-space: nowrap;
}
.logo-bracket { color: var(--accent-1); }
.logo-name { margin: 0 4px; }

.nav-links {
  grid-area: links;
  display: flex;
  gap: 4px;
  justify-content: center;
}
.nav-link {
  text-decoration: none;
  color: var(--text-secondary);
  font-size: 0.9rem;
  font-weight: 500;
  padding: 6px 14px;
  border-radius: 100px;
  transition: all 0.3s;
}
.nav-link:hover, .nav-link.active {
  color: var(--text-primary);
  background: rgba(108,99,255,0.12);
}
.nav-link.active { color: var(--accent-1); }

.nav-actions {
  grid-area: actions;
  display: flex;
  align-items: center;
  gap: 8px;
  flex-shrink: 0;
}
.lang-toggle {
  display: flex;
  align-items: center;
  gap: 6px;
  padding: 8px 16px;
  border-radius: 100px;
  border: 1px solid var(--border-hover);
  background: rgba(108,99,255,0.08);
  color: var(--text-primary);
  cursor: pointer;
  font-size: 0.85rem;
  font-weight: 600;
  transition: all 0.3s;
}
.lang-toggle:hover { background: rgba(108,99,255,0.2); }
.lang-icon { font-size: 1rem; }

.theme-toggle {
  width: 38px;
  height: 38px;
  border-radius: 50%;
  border: 1px solid var(--border-hover);
  background: rgba(108,99,255,0.08);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s;
  flex-shrink: 0;
}
.theme-toggle:hover { background: rgba(108,99,255,0.2); transform: rotate(20deg); }
.theme-icon { font-size: 1.1rem; line-height: 1; }

.icon-flip-enter-active, .icon-flip-leave-active { transition: all 0.25s ease; }
.icon-flip-enter-from { opacity: 0; transform: rotate(-90deg) scale(0.5); }
.icon-flip-leave-to { opacity: 0; transform: rotate(90deg) scale(0.5); }

.hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 4px;
}
.hamburger span {
  display: block;
  width: 24px;
  height: 2px;
  background: var(--text-primary);
  border-radius: 2px;
  transition: all 0.3s;
}
.hamburger.open span:nth-child(1) { transform: rotate(45deg) translate(5px, 5px); }
.hamburger.open span:nth-child(2) { opacity: 0; }
.hamburger.open span:nth-child(3) { transform: rotate(-45deg) translate(5px, -5px); }

.mobile-menu {
  display: flex;
  flex-direction: column;
  padding: 16px 24px 24px;
  border-top: 1px solid var(--border);
  background: rgba(5,5,16,0.95);
}
.mobile-link {
  text-decoration: none;
  color: var(--text-secondary);
  font-size: 1rem;
  font-weight: 500;
  padding: 14px 0;
  border-bottom: 1px solid var(--border);
  transition: color 0.3s;
}
.mobile-link:hover { color: var(--accent-1); }

.mobile-menu-enter-active, .mobile-menu-leave-active { transition: all 0.35s ease; }
.mobile-menu-enter-from, .mobile-menu-leave-to { opacity: 0; transform: translateY(-10px); }

/* ─── Mobile ─── */
@media (max-width: 768px) {
  .nav-links { display: none; }
  .hamburger { display: flex; }
  .navbar { padding: 14px 0; }
  .navbar.scrolled { padding: 10px 0; }
  .nav-inner {
    padding: 0 16px;
    gap: 8px;
    /* Collapse to 2 columns: logo | actions */
    grid-template-columns: auto auto;
    grid-template-areas: 'logo actions';
  }
}

@media (max-width: 480px) {
  .nav-inner { padding: 0 12px; }
  .nav-logo { font-size: 0.92rem; }
  .logo-name { font-size: 0.88rem; }
  .lang-toggle span:last-child { display: none; }
  .lang-toggle { padding: 7px 10px; gap: 0; }
  .theme-toggle { width: 32px; height: 32px; }
  .nav-actions { gap: 6px; }
}
</style>
