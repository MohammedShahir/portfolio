<template>
  <section id="experience" class="section">
    <div class="orb" style="width:400px;height:400px;bottom:0;left:-100px;background:radial-gradient(circle,rgba(108,99,255,0.12),transparent 70%);"></div>
    <div class="container">
      <div class="section-header reveal">
        <div class="section-tag"><span>✦</span> {{ isRtl ? 'المسيرة المهنية' : 'Career Journey' }}</div>
        <h2 class="section-title">{{ isRtl ? 'الخبرات العملية' : 'Professional Experience' }}</h2>
        <p class="section-sub">{{ isRtl ? 'رحلتي المهنية في عالم التقنية والتدريب' : 'My professional journey across tech and training' }}</p>
      </div>

      <div class="timeline">
        <div
          v-for="(exp, i) in d.experience"
          :key="i"
          class="timeline-item reveal"
          :style="{ transitionDelay: `${i * 0.1}s` }"
          @mouseenter="active = i"
          @mouseleave="active = null"
          :class="{ 'is-active': active === i }"
        >
          <div class="tl-dot">
            <div class="tl-dot-inner"></div>
          </div>
          <div class="tl-line"></div>
          <div class="tl-card card">
            <div class="tl-header">
              <div>
                <h3 class="tl-role">{{ exp.role }}</h3>
                <p class="tl-company">
                  <span class="tl-company-name">{{ exp.company }}</span>
                  <span class="tl-sep">·</span>
                  <span class="tl-location">{{ exp.location }}</span>
                </p>
              </div>
              <div class="tl-meta">
                <span class="tag">{{ exp.type }}</span>
                <span class="tl-date">{{ exp.date }}</span>
              </div>
            </div>
            <p class="tl-desc">{{ exp.desc }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
defineProps({ d: Object, isRtl: Boolean })
const active = ref(null)
</script>

<style scoped>
.section-header { margin-bottom: 60px; }

.timeline { position: relative; display: flex; flex-direction: column; gap: 0; }

.timeline-item {
  display: grid;
  grid-template-columns: 40px 1fr;
  gap: 20px;
  position: relative;
  padding-bottom: 8px;
}

.tl-dot {
  display: flex;
  justify-content: center;
  padding-top: 24px;
  z-index: 1;
  flex-shrink: 0;
}
.tl-dot-inner {
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background: var(--bg-secondary);
  border: 2px solid var(--accent-1);
  transition: all 0.35s;
  position: relative;
}
.timeline-item.is-active .tl-dot-inner {
  background: var(--accent-1);
  box-shadow: 0 0 20px rgba(108,99,255,0.6);
  transform: scale(1.3);
}

.tl-line {
  position: absolute;
  left: 19px;
  top: 38px;
  bottom: 0;
  width: 2px;
  background: linear-gradient(to bottom, rgba(108,99,255,0.4), rgba(108,99,255,0.05));
}
.timeline-item:last-child .tl-line { display: none; }

.tl-card { margin-bottom: 24px; }
.timeline-item.is-active .tl-card {
  border-color: rgba(108,99,255,0.35);
  background: rgba(108,99,255,0.04);
}

.tl-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 16px;
  margin-bottom: 12px;
  flex-wrap: wrap;
}
.tl-role { font-size: 1.05rem; font-weight: 700; color: var(--text-primary); margin-bottom: 4px; }
.tl-company { font-size: 0.88rem; color: var(--text-secondary); }
.tl-company-name { font-weight: 600; color: var(--accent-1); }
.tl-sep { margin: 0 6px; color: var(--text-muted); }
.tl-location { color: var(--text-muted); }
.tl-meta { display: flex; flex-direction: column; align-items: flex-end; gap: 6px; flex-shrink: 0; }
.tl-date { font-size: 0.8rem; color: var(--text-muted); white-space: nowrap; }
.tl-desc { font-size: 0.93rem; color: var(--text-secondary); line-height: 1.75; }

.rtl .tl-line { left: auto; right: 19px; }
.rtl .tl-meta { align-items: flex-start; }

@media (max-width: 640px) {
  .tl-header { flex-direction: column; }
  .tl-meta { align-items: flex-start; }
}
</style>
