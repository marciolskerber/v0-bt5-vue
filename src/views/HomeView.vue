<template>
  <main>

    <h1 class="text-center" data-aos="fade-down">{{ t("welcome") }}</h1>
    
    <!-- Adiciona o carrossel -->
    <AppCarousel data-aos="zoom-in" />
    <div class="container py-5" data-aos="fade-up" data-aos-delay="150">
      <h1 class="fw-bold display-5">{{ t("homePage.title") }}</h1>
      <p class="lead text-opacity-75">{{ t("homePage.welcomeMessage") }}</p>
    </div>
  </main>
</template>

<script setup lang="ts">
import { useI18n } from "vue-i18n";
import AppCarousel from "@/components/AppCarousel.vue";

const { t } = useI18n();
</script>
