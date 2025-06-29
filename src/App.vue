<script setup lang="ts">
import { useI18n } from "vue-i18n";
import Navbar from "@/components/NavBar.vue"; // Importe o Navbar.vue
import FooterBar from "@/components/FooterBar.vue";

const { t } = useI18n(); // Remova 'locale' pois não é usado
</script>

<template>
  <div id="app" class="d-flex flex-column min-vh-100">
    <!-- Exibição do texto traduzido (mantido) -->
    <h1 class="text-center">{{ t("welcome") }}</h1>

    <!-- Barra de navegação com o dropdown de idioma estilizado, links e modo escuro -->
    <Navbar />

    <!-- Renderiza as rotas (HomeView, AboutView, ContactsView, etc.) -->
    <!-- Conteúdo principal ocupa todo espaço disponível -->
    <main class="flex-fill container py-4">
      <RouterView />
    </main>

    <!-- Criar rodapé -->
    <FooterBar />
  </div>
</template>
