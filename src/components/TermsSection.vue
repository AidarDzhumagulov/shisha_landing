<script setup>
import { terms } from '../data/content.js'
</script>

<template>
  <section id="terms" class="section-wrap--alt">
    <div class="section-wrap">
      <div class="s-label">Важно знать</div>
      <h2 class="s-title">Условия аренды</h2>
      <div class="s-divider"></div>

      <div class="grid">
        <div v-for="t in terms" :key="t.title" class="term">
          <span class="term-icon">{{ t.icon }}</span>
          <div>
            <div class="term-title">{{ t.title }}</div>
            <div class="term-desc">{{ t.desc }}</div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.grid {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.term {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  padding: 16px 20px;
  display: flex;
  align-items: flex-start;
  gap: 16px;
}
.term-icon { font-size: 22px; flex-shrink: 0; margin-top: 1px; }
.term-title {
  font-size: 14px;
  font-weight: 600;
  color: var(--text-h);
  margin-bottom: 4px;
}
.term-desc { font-size: 13px; color: var(--text); line-height: 1.6; }

@media (min-width: 640px) {
  .grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>
