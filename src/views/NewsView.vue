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
