<script setup lang="ts">
import { ref } from "vue";
import { useI18n } from "vue-i18n";

const { t } = useI18n();
const nome = ref("");
const email = ref("");
const mensagem = ref("");

const enviarFormulario = () => {
  console.log("Nome:", nome.value);
  console.log("Email:", email.value);
  console.log("Mensagem:", mensagem.value);

  //traduz a mensagem e limpa os campos
  showToast();

  nome.value = "";
  email.value = "";
  mensagem.value = "";
};

const showToast = () => {
  const toastEl = document.getElementById("successToast");
  if (toastEl) {
    const toast = new bootstrap.Toast(toastEl);
    toast.show();
  }
};
</script>

<template>
  <div class="container mt-5">
    <div class="row">
      <!-- Coluna: Formulário -->
      <div class="col-md-6 mb-4">
        <div class="contact-form">
          <h2 class="mb-4 text-start">{{ t("contactPage.title") }}</h2>

          <form @submit.prevent="enviarFormulario">
            <div class="mb-3">
              <label for="nome" class="form-label">{{
                t("contactPage.form.nameLabel")
              }}</label>
              <input
                type="text"
                class="form-control"
                id="nome"
                v-model="nome"
                :placeholder="t('contactPage.form.namePlaceholder')"
                required
              />
            </div>

            <div class="mb-3">
              <label for="email" class="form-label">{{
                t("contactPage.form.emailLabel")
              }}</label>
              <input
                type="email"
                class="form-control"
                id="email"
                v-model="email"
                :placeholder="t('contactPage.form.emailPlaceholder')"
                required
              />
            </div>

            <div class="mb-3">
              <label for="mensagem" class="form-label">{{
                t("contactPage.form.messageLabel")
              }}</label>
              <textarea
                id="mensagem"
                class="form-control"
                v-model="mensagem"
                rows="5"
                :placeholder="t('contactPage.form.messagePlaceholder')"
                required
              ></textarea>
            </div>

            <button type="submit" class="btn btn-success w-100">
              {{ t("contactPage.form.submitButton") }}
            </button>
          </form>
        </div>
      </div>

      <!-- Coluna: Mapa -->
      <div class="col-md-6">
        <h3 class="mb-3 text-start">
          {{ $t("contactPage.form.locationTitle") }}
        </h3>
        <div class="mapa-container">
          <iframe
            src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3623.820351132375!2d-53.766341624975766!3d-24.733047105680583!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x94f395bcaf1f4697%3A0x8f229c248dfeae93!2sUTFPR%20-%20Campus%20Toledo!5e0!3m2!1spt-BR!2sbr!4v1750895253053!5m2!1spt-BR!2sbr"
            width="100%"
            height="400"
            style="border: 0"
            loading="lazy"
            referrerpolicy="no-referrer-when-downgrade"
          >
          </iframe>
        </div>
      </div>
    </div>
  </div>

  <div
    class="toast-container position-fixed bottom-0 end-0 p-3"
    style="z-index: 9999"
  >
    <div
      id="successToast"
      class="toast align-items-center text-bg-success border-0"
      role="alert"
      aria-live="assertive"
      aria-atomic="true"
    >
      <div class="d-flex">
        <div class="toast-body">
          {{ t("contactPage.form.successMessage") }}
        </div>
        <button
          type="button"
          class="btn-close btn-close-white me-2 m-auto"
          data-bs-dismiss="toast"
          aria-label="Close"
        ></button>
      </div>
    </div>
  </div>
</template>

<style scoped>
h2 {
  font-size: 2rem;
  margin-bottom: 1.25rem;
}
.contact-form {
  max-width: 30em;
  font-size: 1rem;
}
.form-label {
  font-size: 1rem;
}
input.form-control {
  font-size: 1rem;
  padding: 0.5em;
}
button.btn {
  font-size: 1rem;
  padding: 0.75em 0;
}
.mapa-container {
  max-width: 800px;
  margin: 0 auto;
  text-align: start;
}
</style>
