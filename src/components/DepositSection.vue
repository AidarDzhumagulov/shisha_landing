<script setup>
import { deposits } from '../data/content.js'
</script>

<template>
  <section id="deposit">
    <div class="section-wrap">
      <div class="s-label">Залог</div>
      <h2 class="s-title">Варианты залога</h2>
      <div class="s-divider"></div>
      <p class="s-sub">Выберите удобный вариант — залог возвращается в полном объёме.</p>

      <div class="grid">
        <div v-for="d in deposits" :key="d.title" class="dep-card">
          <div class="dep-icon">{{ d.icon }}</div>
          <div class="dep-title">{{ d.title }}</div>
          <div class="dep-amount">{{ d.amount }}</div>
          <div class="dep-desc">{{ d.desc }}</div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.grid {
  display: flex;
  flex-direction: column;
  gap: 12px;
}
.dep-card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 24px 20px;
  transition: border-color 0.2s, transform 0.2s;
}
@media (hover: hover) {
  .dep-card:hover {
    border-color: var(--gold-border);
    transform: translateY(-2px);
  }
}
.dep-icon { font-size: 28px; margin-bottom: 12px; }
.dep-title {
  font-size: 11px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--gold);
  margin-bottom: 6px;
}
.dep-amount {
  font-size: 28px;
  font-weight: 700;
  color: var(--text-h);
  line-height: 1;
  margin-bottom: 12px;
}
.dep-desc {
  font-size: 14px;
  color: var(--text);
  line-height: 1.65;
  border-top: 1px solid var(--border);
  padding-top: 14px;
}

@media (min-width: 500px) {
  .grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>
