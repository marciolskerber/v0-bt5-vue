<template>
  <main>
    <div class="container py-5">
      <h1>{{ t('homePage.title') }}</h1>
      <p>{{ t('homePage.welcomeMessage') }}</p>
    </div>
    <Footer />
  </main>
</template>

<script setup lang="ts">
import { useI18n } from 'vue-i18n';
import Footer from "@/components/FooterBar.vue";

const { t } = useI18n();
</script>

<style scoped>
h1 {
  font-family: "Oswald", serif;
  font-size: 2rem;
  margin-bottom: 1.5rem;
}
</style>
