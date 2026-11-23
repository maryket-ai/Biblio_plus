<script setup>
const model = defineModel({ type: String, default: '' })
</script>

<template>
  <form class="search" role="search" @submit.prevent>
    <label for="q" class="sr-only">Rechercher un livre</label>
    <input id="q" v-model="model" type="search"
           placeholder="Titre, auteur…" />
  </form>
</template>

<style scoped>
.search {
  width: 100%;
  max-width: 550px;
  margin: 0 auto;
}

.search input {
  width: 100%;
  padding: 15px 20px;
  border: 1px solid #dce3dc;
  border-radius: 30px;
  outline: none;
  background: #ffffff;
  color: #193b2b;
  font-size: 15px;
  box-sizing: border-box;
  transition: all 0.3s ease;
}

.search input::placeholder {
  color: #9a9f9a;
}

.search input:focus {
  border-color: #315c43;
  box-shadow: 0 0 0 3px rgba(49, 92, 67, 0.12);
}
</style>
