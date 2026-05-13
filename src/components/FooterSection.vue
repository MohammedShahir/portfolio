<template>
  <footer class="footer" :class="{ rtl: isRtl }">
    <div class="footer-glow"></div>
    <div class="container footer-inner">
      <div class="footer-brand">
        <a href="#hero" class="footer-logo">
          <span class="logo-bracket">&lt;</span>{{ d.name }}<span class="logo-bracket"> /&gt;</span>
        </a>
        <p class="footer-tagline">{{ d.tagline }}</p>
      </div>
      <div class="footer-links">
        <a v-for="(link, i) in d.navLinks" :key="i" :href="`#${d.navIds[i]}`" class="footer-link">{{ link }}</a>
      </div>
    </div>
    <div class="footer-bottom container">
      <p class="footer-copy">© {{ year }} {{ d.fullName }}. {{ isRtl ? 'جميع الحقوق محفوظة.' : 'All rights reserved.' }}</p>
      <!-- <p class="footer-made">{{ isRtl ? 'صُنع بـ' : 'Built with' }} <span class="heart">♥</span> {{ isRtl ? 'باستخدام Vue.js' : 'using Vue.js' }}</p> -->
    </div>
  </footer>
</template>

<script setup>
defineProps({ d: Object, isRtl: Boolean })
const year = new Date().getFullYear()
</script>

<style scoped>
.footer {
  position: relative;
  padding: 60px 0 0;
  border-top: 1px solid var(--border);
  overflow: hidden;
}
.footer-glow {
  position: absolute;
  top: -1px; left: 50%; transform: translateX(-50%);
  width: 400px; height: 2px;
  background: linear-gradient(90deg, transparent, var(--accent-1), var(--accent-2), transparent);
}
.footer-inner {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 40px;
  flex-wrap: wrap;
  margin-bottom: 48px;
}
.footer-logo {
  font-size: 1.1rem;
  font-weight: 700;
  text-decoration: none;
  color: var(--text-primary);
  margin-bottom: 12px;
  display: block;
}
.logo-bracket { color: var(--accent-1); }
.footer-tagline { font-size: 0.88rem; color: var(--text-muted); max-width: 280px; line-height: 1.7; }
.footer-links { display: flex; flex-direction: column; gap: 10px; }
.footer-link {
  text-decoration: none;
  color: var(--text-secondary);
  font-size: 0.88rem;
  transition: color 0.3s;
}
.footer-link:hover { color: var(--accent-1); }
.footer-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 24px;
  border-top: 1px solid var(--border);
  flex-wrap: wrap;
  gap: 8px;
}
.footer-copy, .footer-made { font-size: 0.8rem; color: var(--text-muted); }
.heart { color: var(--accent-2); animation: heartbeat 1.5s ease infinite; display: inline-block; }
@keyframes heartbeat {
  0%,100% { transform: scale(1); }
  50% { transform: scale(1.3); }
}
@media (max-width: 640px) {
  .footer-bottom { justify-content: center; text-align: center; }
}
</style>
