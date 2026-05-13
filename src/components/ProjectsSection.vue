<template>
  <section id="projects" class="section">
    <div class="orb" style="width:500px;height:500px;top:-50px;left:-100px;background:radial-gradient(circle,rgba(108,99,255,0.1),transparent 70%);"></div>
    <div class="container">
      <div class="section-header reveal">
        <div class="section-tag"><span>✦</span> {{ isRtl ? 'أعمالي' : 'My Work' }}</div>
        <h2 class="section-title">{{ isRtl ? 'المشاريع البرمجية' : 'Featured Projects' }}</h2>
        <p class="section-sub">{{ isRtl ? 'مجموعة من المشاريع التي بنيتها بشغف واحترافية' : 'A selection of projects I built with passion and precision' }}</p>
      </div>

      <div class="projects-grid">
      <a
          v-for="(proj, i) in d.projects"
          :key="i"
          :href="proj.link"
          target="_blank"
          rel="noopener noreferrer"
          class="project-card card reveal"
          :style="{ transitionDelay: `${(i % 3) * 0.1}s` }"
        >
          <div class="proj-top">
            <div class="proj-folder">
              <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M22 19a2 2 0 01-2 2H4a2 2 0 01-2-2V5a2 2 0 012-2h5l2 3h9a2 2 0 012 2z"/></svg>
            </div>
            <div class="proj-link-icon" :title="isRtl ? 'رابط المشروع' : 'View on GitHub'">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>
            </div>
          </div>

          <h3 class="proj-name">{{ proj.name }}</h3>
          <p class="proj-desc">{{ proj.desc }}</p>

          <div class="proj-footer">
            <div class="proj-stack">
              <span v-for="s in proj.stack" :key="s" class="tag">{{ s }}</span>
            </div>
            <span class="proj-date">{{ proj.date }}</span>
          </div>

          <div class="proj-glow"></div>
        </a>
      </div>

      <div class="projects-cta reveal">
        <a :href="d.github" target="_blank" class="btn btn-outline">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>
          {{ isRtl ? 'عرض جميع المشاريع على GitHub' : 'View All Projects on GitHub' }}
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
        </a>
      </div>
    </div>
  </section>
</template>

<script setup>
defineProps({ d: Object, isRtl: Boolean })
</script>

<style scoped>
.section-header { margin-bottom: 60px; }

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: 24px;
  margin-bottom: 48px;
}

.project-card {
  display: flex;
  flex-direction: column;
  gap: 14px;
  cursor: pointer;
  overflow: hidden;
  text-decoration: none;
  color: inherit;
}

.proj-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.proj-folder { color: var(--accent-1); }
.proj-link-icon {
  color: var(--text-muted);
  transition: color 0.3s, transform 0.3s;
  display: flex;
}
.proj-link-icon:hover { color: var(--accent-1); transform: translateY(-2px); }

.proj-name {
  font-size: 1.1rem;
  font-weight: 700;
  color: var(--text-primary);
  transition: color 0.3s;
}
.project-card:hover .proj-name { color: var(--accent-1); }

.proj-desc {
  font-size: 0.88rem;
  color: var(--text-secondary);
  line-height: 1.7;
  flex: 1;
}

.proj-footer {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  gap: 10px;
  flex-wrap: wrap;
  margin-top: auto;
  padding-top: 14px;
  border-top: 1px solid var(--border);
}
.proj-stack { display: flex; flex-wrap: wrap; gap: 6px; }
.proj-date { font-size: 0.78rem; color: var(--text-muted); white-space: nowrap; }

.proj-glow {
  position: absolute;
  bottom: 0; left: 0; right: 0;
  height: 2px;
  background: linear-gradient(90deg, var(--accent-1), var(--accent-2));
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 0.4s ease;
}
.project-card:hover .proj-glow { transform: scaleX(1); }

.projects-cta { display: flex; justify-content: center; }
</style>
