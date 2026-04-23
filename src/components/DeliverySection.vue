<script setup>
import { zones } from '../data/content.js'
import { WA_LINK } from '../constants.js'
</script>

<template>
  <section id="delivery" class="section-wrap--alt">
    <div class="section-wrap">
      <div class="s-label">Доставка</div>
      <h2 class="s-title">Пансионаты</h2>
      <div class="s-divider"></div>
      <p class="s-sub">Доставляем на Иссык-Куль. Стоимость доставки зависит от пансионата.</p>

      <div class="zones">
        <div v-for="zone in zones" :key="zone.name" class="zone">
          <span class="zone-name">{{ zone.name }}</span>
          <span class="zone-price">{{ zone.price }}</span>
        </div>
      </div>

      <div class="note">
        <span class="note-icon">📍</span>
        <div class="note-text">
          <strong>Вашего пансионата нет в списке?</strong>
          Напишите нам — уточним, возможна ли доставка и сколько она будет стоить.
          Доставка в отдалённые места рассматривается индивидуально.
          <a :href="WA_LINK" target="_blank" class="note-link">Написать в WhatsApp →</a>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.zones {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.zone {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  padding: 16px 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  transition: border-color 0.2s;
}
.zone:hover { border-color: var(--gold-border); }
.zone-name {
  font-size: 15px;
  font-weight: 600;
  color: var(--text-h);
}
.zone-price {
  font-size: 15px;
  font-weight: 700;
  color: var(--gold);
  white-space: nowrap;
}

.note {
  margin-top: 16px;
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  padding: 16px 20px;
  display: flex;
  align-items: flex-start;
  gap: 14px;
}
.note-icon { font-size: 20px; flex-shrink: 0; margin-top: 1px; }
.note-text {
  font-size: 14px;
  color: var(--text);
  line-height: 1.65;
}
.note-text strong {
  display: block;
  color: var(--text-h);
  margin-bottom: 4px;
}
.note-link {
  display: inline-block;
  margin-top: 8px;
  color: var(--gold);
  font-weight: 600;
  font-size: 14px;
}
</style>
