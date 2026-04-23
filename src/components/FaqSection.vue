<script setup>
import { faqs } from '../data/content.js'
</script>

<template>
  <section id="faq">
    <div class="section-wrap">
      <div class="s-label">FAQ</div>
      <h2 class="s-title">Частые вопросы</h2>
      <div class="s-divider"></div>

      <div class="faq-list">
        <details v-for="item in faqs" :key="item.q" class="faq-item">
          <summary class="faq-q">
            {{ item.q }}
            <span class="faq-icon" aria-hidden="true">+</span>
          </summary>
          <div class="faq-a">{{ item.a }}</div>
        </details>
      </div>
    </div>
  </section>
</template>

<style scoped>
.faq-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.faq-item {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  overflow: hidden;
  transition: border-color 0.2s;
}
.faq-item[open] { border-color: var(--gold-border); }

.faq-q {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  padding: 18px 20px;
  font-size: 15px;
  font-weight: 600;
  color: var(--text-h);
  cursor: pointer;
  list-style: none;
  user-select: none;
  min-height: 56px;
}
.faq-q::-webkit-details-marker { display: none; }

.faq-icon {
  font-size: 22px;
  font-weight: 300;
  color: var(--gold);
  flex-shrink: 0;
  transition: transform 0.25s;
  line-height: 1;
}
.faq-item[open] .faq-icon { transform: rotate(45deg); }

.faq-a {
  padding: 0 20px 18px;
  font-size: 14px;
  line-height: 1.7;
  color: var(--text);
  border-top: 1px solid var(--border);
  padding-top: 14px;
}
</style>
