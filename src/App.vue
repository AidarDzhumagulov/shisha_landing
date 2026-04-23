<script setup>
import AppNav       from './components/AppNav.vue'
import HeroSection  from './components/HeroSection.vue'
import PricesSection   from './components/PricesSection.vue'
import TobaccoSection  from './components/TobaccoSection.vue'
import DeliverySection from './components/DeliverySection.vue'
import TermsSection    from './components/TermsSection.vue'
import DepositSection  from './components/DepositSection.vue'
import FaqSection      from './components/FaqSection.vue'
import CtaSection      from './components/CtaSection.vue'
import AppFooter       from './components/AppFooter.vue'
</script>

<template>
  <AppNav />
  <main>
    <HeroSection />
    <PricesSection />
    <TobaccoSection />
    <DeliverySection />
    <TermsSection />
    <DepositSection />
    <FaqSection />
    <CtaSection />
  </main>
  <AppFooter />
</template>
