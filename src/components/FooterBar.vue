<template>
  <footer class="pt-4 border-top mt-5 bg-body-secondary text-body">
    <div class="container py-4">
      <div class="row">
        <!-- Institucional -->
        <div class="col-md-4 mb-4">
          <h5 class="fw-bold">{{ t("footer.title") }}</h5>
          <p>{{ t("footer.description") }}</p>
        </div>

        <!-- Contato -->
        <div class="col-md-4 mb-4">
          <h5 class="fw-bold">{{ t("footer.contact") }}</h5>
          <ul class="list-unstyled">
            <li>{{ t("footer.address") }}</li>
            <li>{{ t("footer.phone") }}</li>
            <li>
              <a :href="'mailto:' + t('footer.email')" class="text-decoration-none">
                {{ t("footer.email") }}
              </a>
            </li>
          </ul>
        </div>

        <!-- Redes sociais com imagens locais -->
        <div class="col-md-4 mb-4">
          <h5 class="fw-bold">Social</h5>
          <div class="d-flex flex-wrap gap-2">
            <a
              v-for="(url, name) in socialLinks"
              :key="name"
              :href="url"
              target="_blank"
              rel="noopener"
              class="d-inline-block"
              :aria-label="t('footer.socialMedia.' + name)"
            >
              <img
                :src="getIconPath(name)"
                :alt="name"
                class="social-icon"
              />
            </a>
          </div>
        </div>
      </div>

      <div class="text-center mt-4 small text-muted">
        {{ t("footer.copyright") }}
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
import { useI18n } from "vue-i18n";
const { t } = useI18n();

const socialLinks = {
  twitter: "https://x.com/utfpr_td",
  whatsapp: "tel:+554530801800",
  youtube: "https://www.youtube.com/@UTFPRToledoOficial",
  instagram: "https://www.instagram.com/utfprtd",
  facebook: "https://www.facebook.com/UTFPR.TD/",
  linkedin: "https://br.linkedin.com/company/datcom-utfpr-td",
};

// função para pegar o caminho da imagem da pasta img
const getIconPath = (name: string) => {
  return new URL(`/src/img/${name}.png`, import.meta.url).href;
};
</script>
