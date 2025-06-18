<script setup lang="ts">
import { useI18n } from 'vue-i18n';
const { t } = useI18n();
</script>
<template>
  <div class="container mt-5">
    <h1>{{ t('contactPage.title') }}</h1>
    <p>{{ t('contactPage.content') }}</p>
  </div>
</template>