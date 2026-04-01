<template>
  <div class="contact-container">
    <h1>Formulaire de Contact</h1>
    <form @submit.prevent="submitForm">
      <div class="form-group">
        <label for="name">Nom :</label>
        <input
          id="name"
          v-model="form.name"
          type="text"
          required
          placeholder="Votre nom"
        />
      </div>

      <div class="form-group">
        <label for="email">Email :</label>
        <input
          id="email"
          v-model="form.email"
          type="email"
          required
          placeholder="Votre email"
        />
      </div>

      <div class="form-group">
        <label for="subject">Sujet :</label>
        <input
          id="subject"
          v-model="form.subject"
          type="text"
          required
          placeholder="Sujet du message"
        />
      </div>

      <div class="form-group">
        <label for="message">Message :</label>
        <textarea
          id="message"
          v-model="form.message"
          required
          placeholder="Votre message"
          rows="6"
        ></textarea>
      </div>

      <button type="submit">Envoyer</button>
    </form>

    <div v-if="submitted" class="success-message">
      Merci ! Votre message a été envoyé avec succès.
    </div>
  </div>
</template>

<script>
export default {
  name: 'ContactView',
  data() {
    return {
      form: {
        name: '',
        email: '',
        subject: '',
        message: ''
      },
      submitted: false
    }
  },
  methods: {
    submitForm() {
      console.log('Formulaire soumis:', this.form)
      this.submitted = true
      this.resetForm()
      setTimeout(() => {
        this.submitted = false
      }, 3000)
    },
    resetForm() {
      this.form = {
        name: '',
        email: '',
        subject: '',
        message: ''
      }
    }
  }
}
</script>

<style scoped>
.contact-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 40px 20px;
  font-family: Arial, sans-serif;
}

h1 {
  text-align: center;
  color: #333;
  margin-top: 30px;
  margin-bottom: 30px;
}

form {
  display: flex;
  flex-direction: column;
}

.form-group {
  margin-bottom: 20px;
  display: flex;
  flex-direction: column;
}

label {
  margin-bottom: 8px;
  font-weight: bold;
  color: #555;
}

input,
textarea {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 14px;
  font-family: Arial, sans-serif;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #4caf50;
  box-shadow: 0 0 5px rgba(76, 175, 80, 0.3);
}

button {
  padding: 12px 20px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #45a049;
}

.success-message {
  margin-top: 20px;
  padding: 15px;
  background-color: #d4edda;
  border: 1px solid #c3e6cb;
  border-radius: 4px;
  color: #155724;
  text-align: center;
}
</style>
