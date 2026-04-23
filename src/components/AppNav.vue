<script setup>
import { WA_LINK } from '../constants.js'
</script>

<template>
  <nav class="nav">
    <div class="nav-inner">
      <a href="#" class="logo">
        <span class="logo-icon">◈</span>
        <span>Shisha<strong>Rent</strong></span>
      </a>

      <div class="nav-links">
        <a href="#menu">Цены</a>
        <a href="#tobacco">Табаки</a>
        <a href="#deposit">Залог</a>
        <a href="#faq">FAQ</a>
      </div>

      <a :href="WA_LINK" target="_blank" class="btn btn-outline btn-sm nav-cta">
        Написать
      </a>
    </div>
  </nav>
</template>

<style scoped>
.nav {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 100;
  background: rgba(12, 12, 15, 0.88);
  backdrop-filter: blur(14px);
  -webkit-backdrop-filter: blur(14px);
  border-bottom: 1px solid var(--border);
}
.nav-inner {
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 16px;
  height: 56px;
  display: flex;
  align-items: center;
  gap: 24px;
}
.logo {
  display: flex;
  align-items: center;
  gap: 7px;
  font-size: 17px;
  font-weight: 500;
  color: var(--text-h);
  white-space: nowrap;
  flex-shrink: 0;
}
.logo strong { color: var(--gold); font-weight: 700; }
.logo-icon { color: var(--gold); font-size: 18px; }

.nav-links {
  display: flex;
  gap: 24px;
  flex: 1;
}
.nav-links a {
  font-size: 14px;
  color: var(--text);
  transition: color 0.2s;
}
.nav-links a:hover { color: var(--text-h); }

.nav-cta { margin-left: auto; flex-shrink: 0; }

@media (max-width: 640px) {
  .nav-links { display: none; }
  .nav-inner { gap: 0; }
}
</style>
