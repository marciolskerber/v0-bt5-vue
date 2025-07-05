<script lang="ts" setup>
import { computed, ref, onMounted, watch } from "vue";
import { useRouter } from "vue-router";
import { routes } from "@/router";
import { useI18n } from "vue-i18n";

const router = useRouter();
const { t, locale, availableLocales } = useI18n();

const activeRoute = computed(() => router.currentRoute.value.path);
const isActive = (path: string) => path === activeRoute.value;

// 🔆 Tema claro/escuro com ícone
const darkMode = ref(false);
const detectThemeFromSystem = () => {
  darkMode.value = window.matchMedia("(prefers-color-scheme: dark)").matches;
  applyTheme();
};
const applyTheme = () => {
  document.documentElement.setAttribute(
    "data-bs-theme",
    darkMode.value ? "dark" : "light"
  );
  localStorage.setItem("theme", darkMode.value ? "dark" : "light");
};
watch(darkMode, applyTheme);

// 🌍 Idiomas
const languages = computed(() =>
  availableLocales.map((lang) => ({ code: lang }))
);
const isLanguageOpen = ref(false);
const changeLanguage = (lang: string) => {
  locale.value = lang;
  isLanguageOpen.value = false;
  localStorage.setItem("language", lang);
};

// 🎯 Inicialização
onMounted(() => {
  detectThemeFromSystem();
  window
    .matchMedia("(prefers-color-scheme: dark)")
    .addEventListener("change", detectThemeFromSystem);

  const savedLanguage = localStorage.getItem("language");
  if (savedLanguage && languages.value.some((l) => l.code === savedLanguage)) {
    locale.value = savedLanguage;
  }
});

// 🔍 Busca
const query = ref("");
const filteredRoutes = computed(() =>
  routes.filter((r) =>
    r.children?.some((c) =>
      c.name?.toLowerCase().includes(query.value.toLowerCase())
    )
  )
);
const goToSearch = () => {
  if (query.value.trim()) {
    router.push({ path: "/search", query: { q: query.value } });
    query.value = "";
  }
};
</script>

<template>
  <nav
    data-aos="fade-up"
    class="navbar navbar-expand-lg py-3 shadow-sm fixed-link fw-bold"
  >
    <div class="container">
      <a class="navbar-brand text-white fw-bold" href="#">UTFPR</a>

      <button
        class="navbar-toggler border-0"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div
        id="navbarNav"
        class="collapse navbar-collapse d-flex justify-content-between"
      >
        <!-- 🌐 Rotas -->
        <ul class="navbar-nav">
          <li
            v-for="route in routes.filter((r) => !r.meta?.hidden)"
            :key="route.path"
            class="nav-item text-uppercase"
          >
            <router-link
              :to="route.path"
              class="nav-link text-black fixed-link"
              :class="{ active: isActive(route.path) }"
            >
              {{
                  route.children[0]?.name
                  ? t(`routes.${route.children[0].name.toLowerCase()}`)
                  : ""
              }}
            </router-link>
          </li>
        </ul>

        <!-- 🎛️ Ações -->
        <div class="d-flex align-items-center">
          <!-- 🔍 Campo de busca estilizado -->
          <form @submit.prevent="goToSearch" class="d-flex me-2">
            <input
              v-model="query"
              :placeholder="t('navbar.search')"
              class="form-control rounded-pill"
            />
          </form>

          <!-- 📝 Resultados (opcional) -->
          <ul v-if="query && filteredRoutes.length" class="search-results">
            <li v-for="r in filteredRoutes" :key="r.path">
              {{ t(`routes.${r.children[0].name.toLowerCase()}`) }}
            </li>
          </ul>

          <!-- 🌐 Idiomas -->
          <div class="language-selector ms-3">
            <button
              class="btn btn-outline-secondary dropdown-toggle"
              @click="isLanguageOpen = !isLanguageOpen"
              :aria-expanded="isLanguageOpen"
            >
              {{ t("language") }}:
              <span class="text-success">
                {{ t("languageNames." + locale) }}
              </span>
            </button>

            <ul
              class="dropdown-menu"
              :class="{ show: isLanguageOpen }"
              @click.stop
            >
              <li v-for="lang in languages" :key="lang.code">
                <button
                  class="dropdown-item w-100 text-start"
                  @click="changeLanguage(lang.code)"
                >
                  {{ t("languageNames." + lang.code) }}
                </button>
              </li>
            </ul>
          </div>

          <!-- 🌗 Switch tema com ícones -->
          <div class="form-check form-switch ms-3">
            <input
              id="darkModeSwitch"
              class="form-check-input"
              type="checkbox"
              v-model="darkMode"
            />
            <label class="form-check-label" for="darkModeSwitch">
              <span v-if="darkMode">🌙</span>
              <span v-else>🌞</span>
            </label>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>