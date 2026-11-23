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
/* Style commun à tous les boutons */
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 12px 24px;
  border-radius: 8px;
  font-family: inherit;
  font-size: 14px;
  font-weight: 600;
  text-decoration: none;
  cursor: pointer;
  transition: all 0.3s ease;
  border: 1px solid transparent;
}

/* Bouton principal */
.btn--primary {
  background-color: #193b2b;
  color: #ffffff;
  border-color: #193b2b;
}

.btn--primary:hover {
  background-color: #28563c;
  border-color: #28563c;
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(25, 59, 43, 0.18);
}

/* Bouton secondaire */
.btn--ghost {
  background-color: transparent;
  color: #193b2b;
  border-color: #193b2b;
}

.btn--ghost:hover {
  background-color: #edf3ee;
  color: #193b2b;
  transform: translateY(-2px);
}

/* Accessibilité : navigation au clavier */
.btn:focus-visible {
  outline: 3px solid #a7c8ae;
  outline-offset: 3px;
}

/* Adaptation aux petits écrans */
@media (max-width: 600px) {
  .btn {
    padding: 10px 18px;
    font-size: 13px;
  }
}

</style>
