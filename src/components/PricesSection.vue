<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { packages, included } from '../data/content.js'
import { WA_LINK } from '../constants.js'

const scrollEl = ref(null)
const activeIndex = ref(0)

function onScroll() {
  const el = scrollEl.value
  if (!el) return
  const cardWidth = el.scrollWidth / packages.length
  activeIndex.value = Math.round(el.scrollLeft / cardWidth)
}

function scrollTo(i) {
  const el = scrollEl.value
  if (!el) return
  const cardWidth = el.scrollWidth / packages.length
  el.scrollTo({ left: cardWidth * i, behavior: 'smooth' })
}

onMounted(() => scrollEl.value?.addEventListener('scroll', onScroll, { passive: true }))
onUnmounted(() => scrollEl.value?.removeEventListener('scroll', onScroll))
</script>

<template>
  <section id="menu" class="section-wrap--alt">
    <div class="section-wrap">
      <div class="s-label">Прайс-лист</div>
      <h2 class="s-title">Выберите время</h2>
      <div class="s-divider"></div>
      <p class="s-sub">Всё необходимое уже включено. Просто выбирайте вкус.</p>

      <div class="scroll-wrapper">
        <div class="cards-scroll" ref="scrollEl">
          <div class="cards-track">
            <div
              v-for="pkg in packages"
              :key="pkg.name"
              class="card"
              :class="{ 'card--accent': pkg.accent, 'card--promo': pkg.promo }"
            >
              <div v-if="pkg.accent" class="badge">Популярный</div>
              <div v-else-if="pkg.promo" class="badge badge--promo">Акция</div>
              <div class="card-time">{{ pkg.name }}</div>
              <div v-if="pkg.label" class="card-sublabel">{{ pkg.label }}</div>
              <div class="card-price">
                {{ pkg.price }} <span class="card-curr">сом</span>
              </div>
              <div v-if="pkg.bonus" class="card-bonus">
                <span class="bonus-icon">🥤</span>
                <span>{{ pkg.bonus }}</span>
              </div>
              <ul class="card-features">
                <li><span class="check">✓</span>{{ pkg.fills }}</li>
                <li><span class="check">✓</span>{{ pkg.coals }}</li>
              </ul>
              <a
                :href="WA_LINK"
                target="_blank"
                class="btn card-btn"
                :class="pkg.promo ? 'btn-promo' : pkg.accent ? 'btn-primary' : 'btn-outline'"
              >
                Заказать
              </a>
            </div>
          </div>
        </div>
        <div class="fade-right" aria-hidden="true"></div>
      </div>

      <!-- Dots (mobile only) -->
      <div class="dots" aria-hidden="true">
        <button
          v-for="(pkg, i) in packages"
          :key="i"
          class="dot"
          :class="{ 'dot--active': activeIndex === i }"
          @click="scrollTo(i)"
        />
      </div>

      <div class="time-note">
        <span>🕘</span>
        <span>Заказы на <strong>3 и 6 часов</strong> принимаются только до <strong>21:00</strong>. После — доступны форматы на 12 и 24 часа.</span>
      </div>

      <div class="included">
        <span class="included-label">В комплекте:</span>
        <div class="included-tags">
          <span v-for="item in included" :key="item" class="tag">{{ item }}</span>
        </div>
        <span class="extra-fill">Доп. забивка — <strong>700 сом</strong></span>
      </div>
    </div>
  </section>
</template>

<style scoped>
.scroll-wrapper {
  position: relative;
  margin: 0 -16px;
}

.cards-scroll {
  overflow-x: auto;
  padding: 12px 16px 16px;
  -webkit-overflow-scrolling: touch;
  scrollbar-width: none;
  scroll-snap-type: x mandatory;
}
.cards-scroll::-webkit-scrollbar { display: none; }

.cards-track {
  display: flex;
  gap: 12px;
  width: max-content;
}

/* Fade hint on the right edge */
.fade-right {
  position: absolute;
  top: 0; right: 0; bottom: 0;
  width: 48px;
  background: linear-gradient(to left, var(--bg-section), transparent);
  pointer-events: none;
}

.card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 24px 20px;
  position: relative;
  width: 78vw;
  max-width: 260px;
  flex-shrink: 0;
  display: flex;
  flex-direction: column;
  gap: 4px;
  scroll-snap-align: center;
  transition: border-color 0.2s;
}
.card--accent {
  border-color: var(--gold-border);
  background: linear-gradient(160deg, #1C1910 0%, #141418 100%);
  box-shadow: var(--shadow-gold);
}
.card--promo {
  border-color: rgba(232, 93, 93, 0.55);
  background: linear-gradient(160deg, #2A1518 0%, #141418 75%);
  box-shadow: 0 0 40px rgba(232, 93, 93, 0.18);
}

.badge {
  position: absolute;
  top: -11px;
  left: 50%;
  transform: translateX(-50%);
  background: var(--gold);
  color: #0C0C0F;
  font-size: 11px;
  font-weight: 700;
  padding: 3px 14px;
  border-radius: 20px;
  white-space: nowrap;
  letter-spacing: 0.04em;
}
.badge--promo {
  background: linear-gradient(135deg, #E85D5D 0%, #D9484C 100%);
  color: #fff;
  box-shadow: 0 4px 14px rgba(232, 93, 93, 0.35);
  letter-spacing: 0.08em;
  animation: promoPulse 2.4s ease-in-out infinite;
}
@keyframes promoPulse {
  0%, 100% { transform: translateX(-50%) scale(1); }
  50%      { transform: translateX(-50%) scale(1.06); }
}

.card-bonus {
  display: flex;
  align-items: center;
  gap: 8px;
  background: linear-gradient(135deg, rgba(232, 93, 93, 0.16), rgba(232, 93, 93, 0.05));
  border: 1px solid rgba(232, 93, 93, 0.3);
  color: #FFB0B0;
  font-size: 12px;
  font-weight: 600;
  padding: 8px 12px;
  border-radius: 10px;
  margin-bottom: 14px;
  line-height: 1.3;
}
.bonus-icon { font-size: 16px; flex-shrink: 0; }

.btn-promo {
  background: linear-gradient(135deg, #E85D5D 0%, #D9484C 100%);
  color: #fff;
}
.btn-promo:active { filter: brightness(1.08); }
@media (hover: hover) {
  .btn-promo:hover {
    transform: translateY(-1px);
    box-shadow: 0 8px 24px rgba(232, 93, 93, 0.3);
    filter: brightness(1.05);
  }
}
.card-time {
  font-size: 18px;
  font-weight: 700;
  color: var(--text-h);
}
.card-sublabel {
  font-size: 11px;
  color: var(--gold);
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.07em;
  margin-bottom: 4px;
}
.card-price {
  font-size: 36px;
  font-weight: 700;
  color: var(--text-h);
  line-height: 1;
  margin: 10px 0 16px;
}
.card-curr { font-size: 16px; font-weight: 500; color: var(--text); }

.card-features {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-bottom: 20px;
  flex: 1;
}
.card-features li {
  font-size: 13px;
  color: var(--text);
  display: flex;
  align-items: center;
  gap: 8px;
}
.check { color: var(--gold); font-weight: 700; flex-shrink: 0; }
.card-btn { width: 100%; }

/* Dots */
.dots {
  display: flex;
  justify-content: center;
  gap: 6px;
  margin: 12px 0 20px;
}
.dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  border: none;
  background: var(--border);
  cursor: pointer;
  padding: 0;
  transition: all 0.25s;
}
.dot--active {
  background: var(--gold);
  width: 20px;
  border-radius: 4px;
}

/* Included block */
.included {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 16px 20px;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 12px;
}
.included-label {
  font-size: 13px;
  font-weight: 600;
  color: var(--text);
  white-space: nowrap;
}
.included-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  flex: 1;
}
.tag {
  background: var(--gold-dim);
  border: 1px solid var(--gold-border);
  color: var(--gold);
  font-size: 12px;
  font-weight: 500;
  padding: 4px 12px;
  border-radius: 20px;
}
.extra-fill {
  font-size: 13px;
  color: var(--text);
  white-space: nowrap;
  margin-left: auto;
}
.extra-fill strong { color: var(--text-h); }

.time-note {
  display: flex;
  align-items: flex-start;
  gap: 10px;
  background: rgba(200, 169, 110, 0.06);
  border: 1px solid var(--gold-border);
  border-radius: var(--radius-sm);
  padding: 14px 18px;
  font-size: 14px;
  color: var(--text);
  line-height: 1.6;
  margin-bottom: 12px;
}
.time-note strong { color: var(--text-h); }

/* Desktop: grid */
@media (min-width: 700px) {
  .scroll-wrapper { margin: 0; }
  .cards-scroll { overflow: visible; padding: 0 0 16px; scroll-snap-type: none; }
  .fade-right { display: none; }
  .cards-track {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(190px, 1fr));
    width: auto;
  }
  .card { width: auto; max-width: none; scroll-snap-align: none; }
  .dots { display: none; }
}
</style>
