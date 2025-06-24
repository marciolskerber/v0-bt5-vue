<script setup lang="ts">
import { useI18n } from "vue-i18n";
import Navbar from "@/components/NavBar.vue"; // Importe o Navbar.vue

const { t } = useI18n(); // Remova 'locale' pois não é usado
</script>

<template>
  <div id="app">
    <!-- Exibição do texto traduzido (mantido) -->
    <h1 class="text-center">{{ t("welcome") }}</h1>

    <!-- Barra de navegação com o dropdown de idioma estilizado, links e modo escuro -->
    <Navbar />

    <!-- Renderiza as rotas (HomeView, AboutView, ContactsView, etc.) -->
    <RouterView />
  </div>
</template> 
