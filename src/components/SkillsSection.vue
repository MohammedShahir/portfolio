<template>
  <section id="skills" class="section">
    <div class="orb" style="width:450px;height:450px;top:50%;right:-100px;transform:translateY(-50%);background:radial-gradient(circle,rgba(67,233,123,0.08),transparent 70%);"></div>
    <div class="container">
      <div class="section-header reveal">
        <div class="section-tag"><span>✦</span> {{ isRtl ? 'القدرات التقنية' : 'Technical Arsenal' }}</div>
        <h2 class="section-title">{{ isRtl ? 'المهارات والتقنيات' : 'Skills & Technologies' }}</h2>
        <p class="section-sub">{{ isRtl ? 'التقنيات التي أستخدمها لبناء حلول برمجية متكاملة' : 'Technologies I use to build complete software solutions' }}</p>
      </div>

      <div class="skills-grid">
        <div
          v-for="(items, category) in d.skills"
          :key="category"
          class="skill-category card reveal"
        >
          <h3 class="cat-title">
            <span class="cat-icon">{{ catIcon(category) }}</span>
            {{ category }}
          </h3>
          <div class="skill-tags">
            <div
              v-for="skill in items"
              :key="skill"
              class="skill-pill"
              @mouseenter="hovered = skill"
              @mouseleave="hovered = null"
              :class="{ 'is-hovered': hovered === skill }"
            >
              <span class="skill-dot"></span>
              {{ skill }}
            </div>
          </div>
        </div>
      </div>

      <!-- Tech logos strip -->
      <div class="tech-strip reveal">
        <div class="strip-track">
          <div class="strip-item" v-for="t in techList" :key="t">{{ t }}</div>
          <div class="strip-item" v-for="t in techList" :key="'dup-'+t">{{ t }}</div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
const props = defineProps({ d: Object, isRtl: Boolean })
const hovered = ref(null)

const techList = ['Laravel', 'Vue.js', 'Flutter', 'PHP', 'MySQL', 'JavaScript', 'Git', 'Tailwind', 'Bootstrap', 'Redis', 'Java', 'C++']

function catIcon(cat) {
  const map = {
    'Programming Languages': '💻', 'لغات البرمجة': '💻',
    'Frameworks & Libraries': '⚡', 'الأطر والمكتبات': '⚡',
    'Database & Backend': '🗄️', 'قواعد البيانات والباك إند': '🗄️',
    'Tools & DevOps': '🛠️', 'الأدوات والـ DevOps': '🛠️',
    'Soft Skills': '🤝', 'المهارات الشخصية': '🤝',
    'Certifications': '🏆', 'الشهادات': '🏆',
  }
  return map[cat] || '✦'
}
</script>

<style scoped>
.section-header { margin-bottom: 60px; }

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: 20px;
  margin-bottom: 60px;
}

.skill-category { transition: var(--transition); }
.cat-title {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 0.95rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 16px;
  padding-bottom: 14px;
  border-bottom: 1px solid var(--border);
}
.cat-icon { font-size: 1.2rem; }

.skill-tags { display: flex; flex-wrap: wrap; gap: 10px; }
.skill-pill {
  display: flex;
  align-items: center;
  gap: 7px;
  padding: 7px 14px;
  border-radius: 100px;
  font-size: 0.82rem;
  font-weight: 500;
  background: rgba(255,255,255,0.03);
  border: 1px solid var(--border);
  color: var(--text-secondary);
  cursor: default;
  transition: all 0.25s;
}
.skill-pill:hover, .skill-pill.is-hovered {
  background: rgba(108,99,255,0.12);
  border-color: rgba(108,99,255,0.4);
  color: var(--text-primary);
  transform: translateY(-2px);
}
.skill-dot {
  width: 5px; height: 5px;
  border-radius: 50%;
  background: var(--accent-1);
  flex-shrink: 0;
}
.skill-pill:hover .skill-dot {
  background: var(--accent-2);
  box-shadow: 0 0 6px var(--accent-2);
}

/* ─── Scrolling tech strip ─── */
.tech-strip {
  overflow: hidden;
  padding: 20px 0;
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
  mask-image: linear-gradient(90deg, transparent, black 15%, black 85%, transparent);
}
.strip-track {
  display: flex;
  gap: 48px;
  width: max-content;
  animation: marquee 18s linear infinite;
}
.strip-item {
  font-size: 0.85rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  color: var(--text-muted);
  white-space: nowrap;
  text-transform: uppercase;
  transition: color 0.3s;
}
.strip-item:hover { color: var(--accent-1); }
@keyframes marquee {
  0% { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}
</style>
