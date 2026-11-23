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
  padding: 13px;
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
/* Statut de disponibilité */
.book-card__status {
  display: inline-flex;
  align-self: flex-start;
  margin: 8px 0 0;
  padding: 6px 12px;
  border-radius: 20px;
  background: #e7f2e9;
  color: #28613b;
  font-size: 12px;
  font-weight: 600;
}

/* Livre emprunté */
.book-card__status--off {
  background: #fbeaea;
  color: #a33b3b;
}
/* Bouton favoris */
.book-card__fav {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  align-self: flex-start;
  gap: 6px;
  margin-top: auto;
  padding: 9px 14px;

  background: transparent;
  color: #315c43;
  border: 1px solid #315c43;
  border-radius: 8px;

  font-family: inherit;
  font-size: 13px;
  font-weight: 600;

  cursor: pointer;
  transition: all 0.3s ease;
}

.book-card__fav:hover {
  background: #edf3ee;
  transform: translateY(-2px);
}

/* État favori */
.book-card__fav[aria-pressed="true"] {
  background: #193b2b;
  color: #ffffff;
  border-color: #193b2b;
}

.book-card__fav:focus-visible {
  outline: 3px solid #a7c8ae;
  outline-offset: 3px;
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
