
<script setup>
import { ref } from 'vue'

const nom = ref('')
const email = ref('')
const sujet = ref('')
const message = ref('')
const messageEnvoye = ref(false)

function envoyerMessage() {
  messageEnvoye.value = true

  // Réinitialisation du formulaire
  nom.value = ''
  email.value = ''
  sujet.value = ''
  message.value = ''
}
</script>

<template>
  <main class="contact-page">
    <header class="contact-header">
      <p class="sur-titre">BIBLIO PLUS</p>
      <h1>Contactez-nous</h1>
      <p>
        Une question, une suggestion ou besoin d'aide ?
        Nous sommes à votre écoute.
      </p>
    </header>

    <section class="contact-container">
      <div class="contact-infos">
        <h2>Restons en contact</h2>

        <p>
          N'hésitez pas à nous écrire pour toute demande concernant
          notre bibliothèque et nos services.
        </p>

        <div class="info-item">
          <span>✉️</span>
          <div>
            <h3>Email</h3>
            <p>Contactez-nous par formulaire.</p>
          </div>
        </div>

        <div class="info-item">
          <span>📚</span>
          <div>
            <h3>Notre mission</h3>
            <p>Faciliter l'accès à la lecture et à la connaissance.</p>
          </div>
        </div>
      </div>

      <form class="contact-form" @submit.prevent="envoyerMessage">
        <h2>Envoyer un message</h2>

        <div class="form-group">
          <label for="nom">Nom complet</label>
          <input
            id="nom"
            v-model="nom"
            type="text"
            placeholder="Votre nom"
            required
          />
        </div>

        <div class="form-group">
          <label for="email">Adresse email</label>
          <input
            id="email"
            v-model="email"
            type="email"
            placeholder="exemple@email.com"
            required
          />
        </div>

        <div class="form-group">
          <label for="sujet">Sujet</label>
          <input
            id="sujet"
            v-model="sujet"
            type="text"
            placeholder="Sujet de votre message"
            required
          />
        </div>

        <div class="form-group">
          <label for="message">Votre message</label>
          <textarea
            id="message"
            v-model="message"
            rows="5"
            placeholder="Écrivez votre message ici..."
            required
          ></textarea>
        </div>

        <button type="submit">
          Envoyer le message
        </button>

        <p v-if="messageEnvoye" class="success-message" role="status">
          Votre message a été enregistré dans cette démonstration.
        </p>
      </form>
    </section>
  </main>
</template>

<style scoped>
.contact-page {
  max-width: 1100px;
  margin: auto;
  padding: 48px 24px;
  color: var(--color-text, #222222);
}

.contact-header {
  text-align: center;
  margin-bottom: 45px;
}

.sur-titre {
  font-size: 13px;
  font-weight: 700;
  letter-spacing: 2px;
}

.contact-header h1 {
  font-size: 36px;
  margin: 12px 0;
}

.contact-header p:last-child {
  color: var(--color-muted, #777777);
}

.contact-container {
  display: grid;
  grid-template-columns: 1fr 1.3fr;
  gap: 40px;
  align-items: start;
}

.contact-infos {
  padding: 25px 0;
}

.contact-infos h2,
.contact-form h2 {
  font-size: 23px;
  margin-bottom: 18px;
}

.contact-infos > p {
  line-height: 1.7;
  color: #777777;
}

.info-item {
  display: flex;
  gap: 15px;
  margin-top: 30px;
  align-items: center;
}

.info-item > span {
  font-size: 25px;
}

.info-item h3 {
  font-size: 16px;
  margin-bottom: 5px;
}

.info-item p {
  font-size: 14px;
  color: #777777;
}

.contact-form {
  padding: 30px;
  border: 1px solid #eeeeee;
  border-radius: 12px;
  background: white;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-bottom: 20px;
}

.form-group label {
  font-size: 14px;
  font-weight: 600;
}

.form-group input,
.form-group textarea {
  width: 100%;
  box-sizing: border-box;
  padding: 13px;
  border: 1px solid #dddddd;
  border-radius: 7px;
  font-family: inherit;
  font-size: 14px;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: 2px solid var(--color-primary, #202020);
  outline-offset: 2px;
}

.form-group textarea {
  resize: vertical;
}

.contact-form button {
  width: 100%;
  padding: 14px;
  border: none;
  border-radius: 7px;
  background: var(--color-primary, #202020);
  color: white;
  font-weight: 600;
  cursor: pointer;
}

.success-message {
  margin-top: 18px;
  color: #16834a;
  font-size: 14px;
}

@media (max-width: 700px) {
  .contact-container {
    grid-template-columns: 1fr;
  }

  .contact-header h1 {
    font-size: 28px;
  }

  .contact-form {
    padding: 20px;
  }
}
</style>
