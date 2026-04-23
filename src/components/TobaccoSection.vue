<script setup>
import { tobaccos } from '../data/content.js'
import { WA_LINK } from '../constants.js'
</script>

<template>
  <section id="tobacco">
    <div class="section-wrap">
      <div class="s-label">Ассортимент</div>
      <h2 class="s-title">Наши табаки</h2>
      <div class="s-divider"></div>
      <p class="s-sub">Starline, Black Burn, Darkside. Три уровня крепости на любой вкус.</p>

      <div class="grid">
        <div v-for="cat in tobaccos" :key="cat.level" class="cat-card">
          <div class="cat-header">
            <span class="cat-dot">{{ cat.dot }}</span>
            <div>
              <div class="cat-level" :style="{ color: cat.color }">{{ cat.level }}</div>
              <div class="cat-brand">{{ cat.brand }}</div>
            </div>
          </div>
          <div class="tags">
            <span v-for="item in cat.items" :key="item" class="flavor-tag">{{ item }}</span>
          </div>
        </div>
      </div>

      <div class="note">
        Не нашли нужный вкус? Обновляем ассортимент регулярно —
        <a :href="WA_LINK" target="_blank" class="note-link">спросите в WhatsApp →</a>
      </div>
    </div>
  </section>
</template>

<style scoped>
.grid {
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin-bottom: 20px;
}
.cat-card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 20px;
}
.cat-header {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  margin-bottom: 16px;
}
.cat-dot { font-size: 22px; line-height: 1.2; }
.cat-level { font-size: 15px; font-weight: 700; margin-bottom: 2px; }
.cat-brand { font-size: 12px; color: var(--text); }

.tags { display: flex; flex-wrap: wrap; gap: 8px; }
.flavor-tag {
  background: rgba(255,255,255,0.04);
  border: 1px solid var(--border);
  color: var(--text);
  font-size: 13px;
  padding: 6px 12px;
  border-radius: 20px;
  transition: all 0.18s;
  cursor: default;
}
@media (hover: hover) {
  .flavor-tag:hover {
    background: var(--gold-dim);
    border-color: var(--gold-border);
    color: var(--gold);
  }
}

.note {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  padding: 16px 20px;
  font-size: 14px;
  color: var(--text);
  line-height: 1.6;
}
.note-link {
  color: var(--gold);
  font-weight: 600;
}

@media (min-width: 700px) {
  .grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
  }
}
</style>
