<script setup>
defineProps({
  variant: { type: String, default: 'primary' }, // primary | ghost
  to: { type: [String, Object], default: null },  // lien interne si renseigné
})
</script>

<template>
  <component :is="to ? 'RouterLink' : 'button'" :to="to"
             :class="['btn', 'btn--' + variant]">
    <slot />
  </component>
</template>

<style scoped>
.btn {
  display: inline-block;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  font-size: 1rem;
  text-decoration: none;
  text-align: center;
  cursor: pointer;
  transition: background-color 0.3s ease, color 0.3s ease;
}
</style>
