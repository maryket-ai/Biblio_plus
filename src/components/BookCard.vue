<script setup>
defineProps({
  book: { type: Object, required: true },
  favorite: { type: Boolean, default: false },
})
const emit = defineEmits(['toggle-favorite'])
</script>

<template>
  <article class="book-card">
    <img class="book-card__cover" :src="book.cover" width="200" height="300"
         :alt="'Couverture de ' + book.title" loading="lazy" />
    <div class="book-card__body">
      <h3 class="book-card__title">{{ book.title }}</h3>
      <p class="book-card__author">{{ book.author }}</p>
      <p class="book-card__status"
         :class="{ 'book-card__status--off': !book.available }">
        {{ book.available ? 'Disponible' : 'Emprunté' }}
      </p>
      <button class="book-card__fav" type="button"
              :aria-pressed="favorite"
              @click="emit('toggle-favorite', book.id)">
        {{ favorite ? '★ Retirer des favoris' : '☆ Ajouter aux favoris' }}
      </button>
      <slot name="actions" />
    </div>
  </article>
</template>

<style scoped>

.book-card {
  display: flex;
  flex-direction: column;
  height: 100%;
  overflow: hidden;
  background: #ffffff;
  border: 1px solid #e6e9e3;
  border-radius: 14px;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.book-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 25px rgba(25, 55, 40, 0.12);
}

/* Couverture du livre */
.book-card__cover {
  width: 100%;
  height: 240px;
  object-fit: cover;
  background: #f1f3ee;
}

/* Contenu de la carte */
.book-card__body {
  display: flex;
  flex-direction: column;
  flex: 1;
  gap: 8px;
  padding: 16px;
}

.book-card__title {
  margin: 0;
  color: #193b2b;
  font-size: 17px;
  font-weight: 700;
  line-height: 1.4;
}

.book-card__author {
  margin: 0;
  color: #777f78;
  font-size: 14px;
}

/* Responsive */
@media (max-width: 600px) {
  .book-card__cover {
    height: 200px;
  }

  .book-card__body {
    padding: 12px;
  }
}

</style>
