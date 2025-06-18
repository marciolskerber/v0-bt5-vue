<script setup lang="ts">
import { useI18n } from 'vue-i18n';
const { t } = useI18n();
</script>
<template>
  <div class="container mt-5">
    <h1>{{ t('aboutPage.title') }}</h1>
    <p>{{ t('aboutPage.content') }}</p>
  </div>
</template>