<template>
  <section id="about" class="section">
    <div class="orb" style="width:350px;height:350px;top:0;right:0;background:radial-gradient(circle,rgba(255,101,132,0.1),transparent 70%);"></div>
    <div class="container">
      <div class="about-grid">
        <div class="about-left reveal-left">
          <div class="section-tag">
            <span>✦</span>
            {{ isRtl ? 'عني' : 'About Me' }}
          </div>
          <h2 class="section-title">{{ isRtl ? 'من أنا؟' : 'Who Am I?' }}</h2>
          <p class="about-text">{{ d.about }}</p>

          <div class="about-info">
            <div class="info-item" v-for="item in infoItems" :key="item.label">
              <span class="info-icon">{{ item.icon }}</span>
              <div>
                <span class="info-label">{{ item.label }}</span>
                <span class="info-value">{{ item.value }}</span>
              </div>
            </div>
          </div>

          <div class="about-langs">
            <div v-for="l in d.languages" :key="l.lang" class="lang-item">
              <div class="lang-top">
                <span>{{ l.lang }}</span>
                <span class="lang-level">{{ l.level }}</span>
              </div>
              <div class="lang-bar">
                <div class="lang-fill" :style="{ width: langWidth(l.level) }"></div>
              </div>
            </div>
          </div>
        </div>

        <div class="about-right reveal-right">
          <div class="edu-card card" v-for="(e, i) in d.education" :key="i">
            <div class="edu-icon">🎓</div>
            <div>
              <h4 class="edu-degree">{{ e.degree }}</h4>
              <p class="edu-inst">{{ e.institution }}</p>
              <span class="tag">{{ e.date }}</span>
            </div>
          </div>

          <div class="hobbies-card card">
            <h4 class="card-heading">{{ isRtl ? 'الاهتمامات' : 'Hobbies & Interests' }}</h4>
            <div class="hobbies-grid">
              <div v-for="h in d.hobbies" :key="h" class="hobby-item">{{ h }}</div>
            </div>
          </div>

          <div class="quote-card card">
            <div class="quote-mark">"</div>
            <p class="quote-text">{{ isRtl ? 'التقنية ليست مجرد أداة، إنها لغة المستقبل.' : 'Technology is not just a tool, it\'s the language of the future.' }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue'
const props = defineProps({ d: Object, isRtl: Boolean })

const infoItems = computed(() => [
  { icon: '📧', label: props.isRtl ? 'البريد الإلكتروني' : 'Email', value: props.d.email },
  { icon: '📱', label: props.isRtl ? 'الهاتف' : 'Phone', value: props.d.phone },
  { icon: '📍', label: props.isRtl ? 'الموقع' : 'Location', value: props.d.location },
])

function langWidth(level) {
  const map = { 'Native': '100%', 'لغة أم': '100%', 'Very Good': '80%', 'جيد جداً': '80%', 'Fair': '50%', 'مقبول': '50%' }
  return map[level] || '60%'
}
</script>

<style scoped>
.about-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  align-items: start;
}
.about-text {
  color: var(--text-secondary);
  font-size: 1.05rem;
  line-height: 1.9;
  margin-bottom: 32px;
}
.about-info { display: flex; flex-direction: column; gap: 16px; margin-bottom: 32px; }
.info-item {
  display: flex;
  align-items: center;
  gap: 14px;
  padding: 14px 18px;
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  transition: border-color 0.3s;
}
.info-item:hover { border-color: var(--border-hover); }
.info-icon { font-size: 1.3rem; }
.info-label { display: block; font-size: 0.75rem; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.1em; margin-bottom: 2px; }
.info-value { font-size: 0.95rem; font-weight: 500; color: var(--text-primary); }

.about-langs { display: flex; flex-direction: column; gap: 16px; }
.lang-item {}
.lang-top { display: flex; justify-content: space-between; margin-bottom: 8px; font-size: 0.9rem; font-weight: 600; }
.lang-level { color: var(--text-muted); font-weight: 400; }
.lang-bar { height: 5px; background: rgba(255,255,255,0.06); border-radius: 3px; overflow: hidden; }
.lang-fill { height: 100%; border-radius: 3px; background: linear-gradient(90deg, var(--accent-1), var(--accent-2)); transition: width 1.5s ease; }

.about-right { display: flex; flex-direction: column; gap: 20px; }
.edu-card { display: flex; align-items: flex-start; gap: 18px; }
.edu-icon { font-size: 1.8rem; flex-shrink: 0; }
.edu-degree { font-size: 1rem; font-weight: 700; color: var(--text-primary); margin-bottom: 4px; }
.edu-inst { font-size: 0.88rem; color: var(--text-secondary); margin-bottom: 10px; }

.card-heading { font-size: 1rem; font-weight: 700; margin-bottom: 16px; color: var(--text-primary); }
.hobbies-grid { display: flex; flex-wrap: wrap; gap: 10px; }
.hobby-item {
  padding: 8px 16px;
  background: rgba(108,99,255,0.08);
  border: 1px solid rgba(108,99,255,0.15);
  border-radius: 100px;
  font-size: 0.85rem;
  transition: all 0.3s;
}
.hobby-item:hover { background: rgba(108,99,255,0.18); transform: scale(1.05); }

.quote-card { border-color: rgba(108,99,255,0.2); background: linear-gradient(135deg, rgba(108,99,255,0.05), transparent); }
.quote-mark { font-size: 4rem; line-height: 1; color: var(--accent-1); opacity: 0.5; font-family: Georgia, serif; margin-bottom: -16px; }
.quote-text { font-style: italic; color: var(--text-secondary); font-size: 1rem; }

@media (max-width: 900px) {
  .about-grid { grid-template-columns: 1fr; }
}
</style>
