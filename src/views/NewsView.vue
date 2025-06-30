<template>
  <div class="container py-4">
    <div id="newsCarousel" class="carousel slide" data-bs-ride="carousel">
      <div class="carousel-inner">
        <div
          class="carousel-item"
          :class="{ active: index === 0 }"
          v-for="(chunk, index) in chunkedNews"
          :key="index"
        >
          <div class="row">
            <div class="col-md-4" v-for="news in chunk" :key="news.id">
              <div class="card h-100 shadow-sm" v-on:click="openLink(news.link)">
                <img :src="news.image" class="card-img-top" :alt="news.title" />
                <div class="card-body d-flex flex-column">
                  <h5 class="card-title">{{ news.title }}</h5>
                  <p class="text-muted mb-1">
                    <i class="bi bi-clock"></i> {{ news.date }}
                  </p>
                  <p class="card-text">{{ news.description }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <button class="carousel-control-prev" type="button" data-bs-target="#newsCarousel" data-bs-slide="prev">
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Anterior</span>
      </button>
      <button class="carousel-control-next" type="button" data-bs-target="#newsCarousel" data-bs-slide="next">
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Próximo</span>
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { useI18n } from "vue-i18n"

const { t } = useI18n()

const newsList = computed(() => [
  {
    id: 1,
    title: t('newsPage.firstNews.title'),
    date: '27/06/2025 15h46',
    description: t('newsPage.firstNews.description'),
    image: 'https://www.utfpr.edu.br/noticias/geral/utfpr-firma-parceria-de-r-39-milhoes-com-petrolifera-chinesa-para-pesquisa-tecnologica/@@images/image',
    link: 'https://www.utfpr.edu.br/noticias/geral/utfpr-firma-parceria-de-r-39-milhoes-com-petrolifera-chinesa-para-pesquisa-tecnologica'
  },
  {
    id: 2,
    title: t('newsPage.secondNews.title'),
    date: '27/06/2025 13h03',
    description: t('newsPage.secondNews.description'),
    image: 'https://www.utfpr.edu.br/noticias/geral/cerimonia-de-posse-da-vice-reitoria-sera-na-proxima-segunda-30/@@images/image',
    link: 'https://www.utfpr.edu.br/noticias/geral/cerimonia-de-posse-da-vice-reitoria-sera-na-proxima-segunda-30'
  },
  {
    id: 3,
    title: t('newsPage.thirdNews.title'),
    date: '27/06/2025 11h28',
    description: t('newsPage.thirdNews.description'),
    image: 'https://www.utfpr.edu.br/noticias/geral/servidores/nota-de-pesar-jose-sollak/@@images/image',
    link: 'https://www.utfpr.edu.br/noticias/geral/servidores/nota-de-pesar-jose-sollak'
  },
  {
    id: 4,
    title: t('newsPage.fourthNews.title'),
    date: '27/06/2025 10h51',
    description: t('newsPage.fourthNews.description'),
    image: 'https://www.utfpr.edu.br/noticias/geral/divulgacao-cientifica/pesquisador-integra-grupo-de-cientistas-a-usar-o-maior-telescopio-do-mundo/@@images/image',
    link: 'https://www.utfpr.edu.br/noticias/geral/divulgacao-cientifica/pesquisador-integra-grupo-de-cientistas-a-usar-o-maior-telescopio-do-mundo'
  },
  {
    id: 5,
    title: t('newsPage.fifthNews.title'),
    date: '25/06/2025 13h50',
    description: t('newsPage.fifthNews.description'),
    image: 'https://www.utfpr.edu.br/noticias/geral/divulgacao-cientifica/pesquisa-revela-que-producao-ecologica-e-a-mais-rentavel-para-agricultura-familiar/@@images/image',
    link: 'https://www.utfpr.edu.br/noticias/geral/divulgacao-cientifica/pesquisa-revela-que-producao-ecologica-e-a-mais-rentavel-para-agricultura-familiar'
  },
  {
    id: 6,
    title: t('newsPage.sixtiethNews.title'),
    date: '25/06/2025 10h02',
    description: t('newsPage.sixtiethNews.description'),
    image: 'https://www.utfpr.edu.br/noticias/geral/servidores/proppg-lanca-edital-inedito-para-registro-de-bolsas-externas-de-iniciacao-cientifica-e-tecnologica/@@images/image',
    link: 'https://www.utfpr.edu.br/noticias/geral/servidores/proppg-lanca-edital-inedito-para-registro-de-bolsas-externas-de-iniciacao-cientifica-e-tecnologica'
  }
])

function openLink(link) {
  window.open(link)
}

const chunkedNews = computed(() => {
  const chunkSize = 3
  const chunks = []
  for (let i = 0; i < newsList.value.length; i += chunkSize) {
    chunks.push(newsList.value.slice(i, i + chunkSize))
  }
  return chunks
})

</script>

<style scoped>
.card-title {
  font-weight: bold;
}
.carousel-control-prev-icon,
.carousel-control-next-icon {
  background-image: none;
  color: white;
  font-size: 5rem;
}

.carousel-control-prev::after,
.carousel-control-next::after {
  content: '‹';
  color: white;
  font-size: 5rem;
  font-weight: bold;
}

.carousel-control-next::after {
  content: '›';
}

.card{
  cursor: pointer;
}

</style>
