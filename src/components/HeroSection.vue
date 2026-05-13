<template>
  <section id="hero" class="hero-section">
    <!-- Animated background grid -->
    <div class="grid-bg"></div>

    <!-- Orbs -->
    <div class="orb" style="width:500px;height:500px;top:-100px;left:-150px;background:radial-gradient(circle,rgba(108,99,255,0.25),transparent 70%);animation-duration:10s;"></div>
    <div class="orb" style="width:400px;height:400px;bottom:-50px;right:-100px;background:radial-gradient(circle,rgba(255,101,132,0.2),transparent 70%);animation-duration:8s;animation-delay:-3s;"></div>

    <div class="hero-inner container">
      <div class="hero-content reveal">
        <div class="hero-badge">
          <span class="badge-dot"></span>
          <span>{{ isRtl ? 'متاح للعمل' : 'Available for work' }}</span>
        </div>

        <h1 class="hero-title">
          <span class="greeting">{{ isRtl ? 'مرحباً، أنا' : "Hi, I'm" }}</span>
          <br />
          <span class="hero-name">{{ d.name }}</span>
        </h1>

        <div class="hero-typewriter">
          <span class="typewriter-text">{{ currentTitle }}</span>
          <span class="cursor">|</span>
        </div>

        <p class="hero-tagline">{{ d.tagline }}</p>

        <div class="hero-actions">
          <a :href="`#contact`" class="btn btn-primary">
            <span>{{ isRtl ? 'تواصل معي' : "Let's Talk" }}</span>
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
          </a>
          <a :href="d.github" target="_blank" class="btn btn-outline">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>
            GitHub
          </a>
        </div>

        <div class="hero-stats">
          <div class="stat">
            <span class="stat-num">6+</span>
            <span class="stat-label">{{ isRtl ? 'مشاريع' : 'Projects' }}</span>
          </div>
          <div class="stat-divider"></div>
          <div class="stat">
            <span class="stat-num">3+</span>
            <span class="stat-label">{{ isRtl ? 'سنوات خبرة' : 'Years Exp.' }}</span>
          </div>
          <div class="stat-divider"></div>
          <div class="stat">
            <span class="stat-num">8+</span>
            <span class="stat-label">{{ isRtl ? 'تقنيات' : 'Technologies' }}</span>
          </div>
        </div>
      </div>

      <div class="hero-visual reveal-right">
        <div class="avatar-wrapper">
          <div class="avatar-ring ring-1"></div>
          <div class="avatar-ring ring-2"></div>
          <div class="avatar-ring ring-3"></div>
          <div class="avatar-main">
            <div class="avatar-initials">MS</div>
            <div class="avatar-glow"></div>
          </div>
          <!-- Floating skill badges -->
          <div class="float-badge badge-laravel" style="top:-10px;right:-20px;">
            <span>🔥 Laravel</span>
          </div>
          <div class="float-badge badge-flutter" style="bottom:10px;left:-30px;">
            <span>📱 Flutter</span>
          </div>
          <div class="float-badge badge-vue" style="top:60%;right:-40px;">
            <span>⚡ Vue.js</span>
          </div>
        </div>
      </div>
    </div>

    <!-- Scroll indicator -->
    <div class="scroll-indicator">
      <div class="scroll-mouse">
        <div class="scroll-wheel"></div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted, watch } from 'vue'
const props = defineProps({ d: Object, isRtl: Boolean })

const titles = [props.d.title]
const currentTitle = ref('')
let charIndex = 0
let timer = null

function type() {
  if (charIndex < props.d.title.length) {
    currentTitle.value += props.d.title[charIndex++]
    timer = setTimeout(type, 60)
  }
}

watch(() => props.d.title, (val) => {
  currentTitle.value = ''
  charIndex = 0
  clearTimeout(timer)
  type()
})

onMounted(() => { type() })
onUnmounted(() => clearTimeout(timer))
</script>

<style scoped>
.hero-section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  position: relative;
  overflow: hidden;
  padding-top: 80px;
}

.grid-bg {
  position: absolute;
  inset: 0;
  background-image: linear-gradient(rgba(108,99,255,0.07) 1px, transparent 1px),
    linear-gradient(90deg, rgba(108,99,255,0.07) 1px, transparent 1px);
  background-size: 60px 60px;
  mask-image: radial-gradient(ellipse 80% 80% at 50% 50%, black, transparent);
}

.hero-inner {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  align-items: center;
  position: relative;
  z-index: 1;
  padding-top: 40px;
  padding-bottom: 80px;
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 6px 16px;
  border-radius: 100px;
  border: 1px solid rgba(67,233,123,0.25);
  background: rgba(67,233,123,0.06);
  color: #43e97b;
  font-size: 0.82rem;
  font-weight: 600;
  margin-bottom: 24px;
}
.badge-dot {
  width: 7px; height: 7px;
  border-radius: 50%;
  background: #43e97b;
  animation: pulse-green 2s infinite;
}
@keyframes pulse-green {
  0%,100% { box-shadow: 0 0 0 0 rgba(67,233,123,0.4); }
  50% { box-shadow: 0 0 0 8px rgba(67,233,123,0); }
}

.greeting {
  display: block;
  font-size: clamp(1rem, 2.5vw, 1.3rem);
  font-weight: 400;
  color: var(--text-secondary);
  margin-bottom: 8px;
}
.hero-title {
  font-size: clamp(2.5rem, 6vw, 4.5rem);
  font-weight: 900;
  line-height: 1;
  margin-bottom: 16px;
}
.hero-name {
  background: linear-gradient(135deg, #f0f0ff, var(--accent-1) 50%, var(--accent-2));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  background-size: 200% 100%;
  animation: shimmer 4s linear infinite;
}
@keyframes shimmer {
  0% { background-position: 0% 50%; }
  100% { background-position: 200% 50%; }
}

.hero-typewriter {
  font-size: clamp(1rem, 2.5vw, 1.25rem);
  color: var(--accent-1);
  font-weight: 600;
  margin-bottom: 20px;
  min-height: 2em;
}
.cursor {
  display: inline-block;
  animation: blink 1s step-end infinite;
  margin-left: 2px;
  color: var(--accent-2);
}
@keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

.hero-tagline {
  color: var(--text-secondary);
  font-size: 1.05rem;
  max-width: 480px;
  margin-bottom: 36px;
  line-height: 1.8;
}

.hero-actions { display: flex; gap: 14px; flex-wrap: wrap; margin-bottom: 48px; }

.hero-stats { display: flex; align-items: center; gap: 20px; }
.stat { text-align: center; }
.stat-num {
  display: block;
  font-size: 1.8rem;
  font-weight: 800;
  background: linear-gradient(135deg, var(--accent-1), var(--accent-2));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
.stat-label { font-size: 0.8rem; color: var(--text-muted); font-weight: 500; }
.stat-divider { width: 1px; height: 40px; background: var(--border); }

/* ─── Avatar ─── */
.hero-visual { display: flex; justify-content: center; align-items: center; }
.avatar-wrapper { position: relative; width: 300px; height: 300px; }
.avatar-main {
  position: absolute;
  inset: 40px;
  border-radius: 50%;
  background: linear-gradient(135deg, #1a1a3a, #0d0d22);
  display: flex;
  align-items: center;
  justify-content: center;
  border: 2px solid rgba(108,99,255,0.3);
  overflow: hidden;
}
.avatar-initials {
  font-size: 4rem;
  font-weight: 900;
  background: linear-gradient(135deg, var(--accent-1), var(--accent-2));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
.avatar-glow {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 50% 50%, rgba(108,99,255,0.15), transparent 70%);
  animation: pulse-glow 3s ease-in-out infinite;
}
@keyframes pulse-glow {
  0%,100% { opacity: 0.5; transform: scale(1); }
  50% { opacity: 1; transform: scale(1.05); }
}

.avatar-ring {
  position: absolute;
  border-radius: 50%;
  border: 1px solid rgba(108,99,255,0.15);
  top: 50%; left: 50%;
  transform: translate(-50%, -50%);
  animation: spin-ring linear infinite;
}
.ring-1 { width: 260px; height: 260px; animation-duration: 20s; border-color: rgba(108,99,255,0.2); }
.ring-2 { width: 300px; height: 300px; animation-duration: 30s; animation-direction: reverse; border-style: dashed; }
.ring-3 { width: 340px; height: 340px; animation-duration: 25s; border-color: rgba(255,101,132,0.1); }
@keyframes spin-ring { to { transform: translate(-50%,-50%) rotate(360deg); } }

.float-badge {
  position: absolute;
  background: rgba(10,10,31,0.9);
  border: 1px solid rgba(108,99,255,0.3);
  border-radius: 100px;
  padding: 6px 14px;
  font-size: 0.78rem;
  font-weight: 600;
  color: var(--text-primary);
  backdrop-filter: blur(10px);
  white-space: nowrap;
  animation: floatBadge 4s ease-in-out infinite;
}
.badge-laravel { animation-delay: 0s; }
.badge-flutter { animation-delay: -1.5s; }
.badge-vue { animation-delay: -3s; }
@keyframes floatBadge {
  0%,100% { transform: translateY(0); }
  50% { transform: translateY(-8px); }
}

/* ─── Scroll Indicator ─── */
.scroll-indicator {
  position: absolute;
  bottom: 32px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  animation: fadeInUp 1s ease 1s both;
}
.scroll-mouse {
  width: 24px; height: 38px;
  border: 2px solid rgba(255,255,255,0.2);
  border-radius: 12px;
  display: flex;
  justify-content: center;
  padding-top: 6px;
}
.scroll-wheel {
  width: 4px; height: 8px;
  border-radius: 2px;
  background: var(--accent-1);
  animation: scroll-bounce 2s ease-in-out infinite;
}
@keyframes scroll-bounce {
  0% { transform: translateY(0); opacity: 1; }
  100% { transform: translateY(14px); opacity: 0; }
}
@keyframes fadeInUp {
  from { opacity: 0; transform: translateX(-50%) translateY(20px); }
  to { opacity: 1; transform: translateX(-50%) translateY(0); }
}

@media (max-width: 900px) {
  .hero-inner { grid-template-columns: 1fr; text-align: center; }
  .hero-visual { order: -1; }
  .hero-actions { justify-content: center; }
  .hero-stats { justify-content: center; }
  .hero-tagline { margin: 0 auto 36px; }
  .hero-badge { margin: 0 auto 24px; }
}
</style>
