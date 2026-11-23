
<script setup>
import { ref, computed, onMounted } from 'vue'
import SearchBar from '@/components/SearchBar.vue'
import BookList from '@/components/BookList.vue'


const books = ref([])
const query = ref('')
const selectedCategory = ref('Toutes')
const selectedSort = ref('title')
const loading = ref(true)
const error = ref(false)

// Charger les livres
onMounted(async () => {
  try {
    const response = await fetch(
      import.meta.env.BASE_URL + 'data/books.json'
    )

    if (!response.ok) {
      throw new Error('Erreur lors du chargement des livres')
    }

    books.value = await response.json()
  } catch (err) {
    console.error(err)
    error.value = true
  } finally {
    loading.value = false
  }
})

// Récupérer automatiquement les catégories
const categories = computed(() => {
  const uniqueCategories = [
    ...new Set(books.value.map(book => book.category))
  ]

  return ['Toutes', ...uniqueCategories]
})

// Rechercher, filtrer et trier les livres
const filteredBooks = computed(() => {
  let result = books.value.filter(book => {
    const search = query.value.toLowerCase().trim()

    const matchesSearch =
      book.title.toLowerCase().includes(search) ||
      book.author.toLowerCase().includes(search)

    const matchesCategory =
      selectedCategory.value === 'Toutes' ||
      book.category === selectedCategory.value

    return matchesSearch && matchesCategory
  })

  // Tri des livres
  if (selectedSort.value === 'title') {
    result.sort((a, b) => a.title.localeCompare(b.title))
  }

  if (selectedSort.value === 'year') {
    result.sort((a, b) => b.year - a.year)
  }

  if (selectedSort.value === 'available') {
    result.sort((a, b) => Number(b.available) - Number(a.available))
  }

  return result
})
</script>

<template>
  <main class="catalogue">

    <!-- INTRODUCTION -->
    <section class="catalogue__hero">
      <p class="section-eyebrow">NOTRE COLLECTION</p>

      <h1>
        À chaque curiosité,<br />
        son livre.
      </h1>

      <p>
        Des histoires, des connaissances et des découvertes :
        trouvez le livre qui vous correspond.
      </p>
    </section>

    <!-- RECHERCHE -->
    <section class="catalogue__search">
      <SearchBar v-model="query" />
    </section>

    <!-- FILTRES -->
    <section class="catalogue__filters">
      <div class="categories">
        <button
          v-for="category in categories"
          :key="category"
          type="button"
          :class="{
            active: selectedCategory === category
          }"
          @click="selectedCategory = category"
        >
          {{ category }}
        </button>
      </div>

      <div class="catalogue__sort">
        <label for="sort">Trier par :</label>

        <select id="sort" v-model="selectedSort">
          <option value="title">Titre (A-Z)</option>
          <option value="year">Plus récents</option>
          <option value="available">Disponibilité</option>
        </select>
      </div>
    </section>

    <!-- LISTE DES LIVRES -->
    <section class="catalogue__books" aria-labelledby="books-title">

      <div class="catalogue__heading">
        <h2 id="books-title">Tous les livres</h2>

        <span>
          {{ filteredBooks.length }} résultat(s)
        </span>
      </div>

      <p v-if="loading">
        Chargement du catalogue...
      </p>

      <p v-else-if="error" role="alert">
        Impossible de charger le catalogue.
      </p>

      <p v-else-if="filteredBooks.length === 0">
        Aucun livre ne correspond à votre recherche.
      </p>

      <BookList v-else :books="filteredBooks" />

    </section>

  </main>
</template>

<style scoped>
.catalogue {
  background: var(--color-background);
  color: var(--color-text);
  padding: 3rem 7%;
  min-height: 70vh;
}

/* INTRODUCTION */
.catalogue__hero {
  margin-bottom: 2rem;
}

.section-eyebrow {
  font-size: 0.7rem;
  letter-spacing: 0.15em;
  color: var(--color-muted);
  font-weight: 600;
}

.catalogue__hero h1 {
  font-family: Georgia, serif;
  font-weight: 400;
  font-size: clamp(2.2rem, 4vw, 3rem);
  line-height: 1.15;
  margin: 1rem 0;
}

.catalogue__hero > p:last-child {
  color: var(--color-muted);
  line-height: 1.7;
}

/* RECHERCHE */
.catalogue__search {
  max-width: 100%;
  margin-bottom: 1.5rem;
}

/* FILTRES */
.catalogue__filters {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  flex-wrap: wrap;
  padding-bottom: 1.5rem;
  border-bottom: 1px solid var(--color-border);
}

.categories {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.categories button {
  padding: 0.6rem 1rem;
  border: 1px solid var(--color-border);
  background: transparent;
  color: var(--color-text);
  cursor: pointer;
  font-size: 0.8rem;
}

.categories button.active {
  background: var(--color-primary);
  color: var(--color-primary-contrast);
  border-color: var(--color-primary);
}

.catalogue__sort {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.8rem;
}

.catalogue__sort select {
  padding: 0.6rem;
  border: 1px solid var(--color-border);
  background: var(--color-surface);
  color: var(--color-text);
}

/* LIVRES */
.catalogue__books {
  padding-top: 2rem;
}

.catalogue__heading {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 1rem;
}

.catalogue__heading h2 {
  font-family: Georgia, serif;
  font-weight: 400;
  font-size: 1.5rem;
}

.catalogue__heading span {
  color: var(--color-muted);
  font-size: 0.8rem;
}

@media (max-width: 650px) {
  .catalogue {
    padding: 2rem 5%;
  }

  .catalogue__filters {
    align-items: flex-start;
    flex-direction: column;
  }

  .catalogue__sort {
    width: 100%;
    justify-content: space-between;
  }
}
</style>
