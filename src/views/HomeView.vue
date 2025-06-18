<template>
  <main>
    <section class="container py-5" > 
      <transition name="fade">
        <div>
          <h1 class="mb-4 text-start">Sobre nós</h1>

          <div class="about-text">
            <p>
              Este site foi desenvolvido como parte da disciplina
              <strong>Web Front-End II</strong> da UTFPR, utilizando Vue 3,
              Vite, TypeScript, Beercss e i18n.
            </p>

            <p>
              O projeto demonstra boas práticas de front-end, com suporte a
              múltiplos idiomas, formulário funcional e responsividade.
            </p>

            <p>
              Desenvolvido por <strong>Vinícius Tabarão</strong>, aluno UTFPR.
            </p>
          </div>

          <div class="contact-form mt-5">
            <h2 class="mb-4 text-start">Fale conosco</h2>

            <form @submit.prevent="enviarFormulario">
              <div class="mb-3">
                <label for="nome" class="form-label">Nome</label>
                <input
                  type="text"
                  class="form-control"
                  id="nome"
                  v-model="nome"
                  placeholder="Digite seu nome"
                  required
                />
              </div>

              <div class="mb-3">
                <label for="email" class="form-label">Email</label>
                <input
                  type="email"
                  class="form-control"
                  id="email"
                  v-model="email"
                  placeholder="email@exemplo.com"
                  required
                />
              </div>

              <button type="submit" class="btn btn-success w-100">
                Enviar
              </button>
            </form>
          </div>
        </div>
      </transition>
    </section>

    <Footer />
  </main>
</template>

<script setup lang="ts">
import { ref } from "vue";
import Footer from "@/components/FooterBar.vue";

const nome = ref("");
const email = ref("");

const enviarFormulario = () => {
  console.log("Nome:", nome.value);
  console.log("Email:", email.value);
  alert("Mensagem enviada com sucesso!");
};
</script>

<style scoped>


h1, h2 {
  font-family: "Oswald", serif;
  text-align: left;
}

h1 {
  font-size: 2rem;
  margin-bottom: 1.5rem;
}

h2 {
  font-size: 1.5rem;
  margin-bottom: 1.25rem;
}

.about-text {
  font-size: 1rem;
  line-height: 1.5rem;
  text-align: left;
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

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.6s ease, transform 0.6s ease;
}

.fade-enter-from {
  opacity: 0;
  transform: translateY(30px);
}

.fade-enter-to {
  opacity: 1;
  transform: translateY(0);
}
</style>
