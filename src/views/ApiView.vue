<template>
  <v-container class="api-container" max-width="960">
    <v-card elevation="2" class="pa-6">
      <v-card-title class="text-h5 justify-center">API REST - exemples JSONPlaceholder</v-card-title>

      <div class="mb-4 d-flex justify-space-between align-center">
        <div>Chargement : <strong>{{ loading ? 'En cours...' : 'Terminé' }}</strong></div>
        <v-btn color="primary" @click="loadPosts" :loading="loading">Rafraîchir</v-btn>
      </div>

      <v-alert v-if="error" type="error" dense>
        Erreur API : {{ error }}
      </v-alert>

      <v-row>
        <v-col cols="12" md="6" lg="4" v-for="post in posts" :key="post.id">
          <v-card class="pa-3" outlined>
            <v-card-title class="text-subtitle-1 font-weight-bold">{{ post.title }}</v-card-title>
            <v-card-text>{{ post.body }}</v-card-text>
          </v-card>
        </v-col>
      </v-row>

      <v-skeleton-loader v-if="loading" type="card" class="mt-4" :loading="loading" />
    </v-card>
  </v-container>
</template>

<script>
export default {
  name: 'ApiView',
  data() {
    return {
      posts: [],
      loading: false,
      error: null
    }
  },
  methods: {
    async loadPosts() {
      this.loading = true
      this.error = null
      try {
        const start = Math.floor(Math.random() * 88)
        const response = await fetch(`https://jsonplaceholder.typicode.com/posts?_start=${start}&_limit=12`)
        if (!response.ok) {
          throw new Error(`HTTP ${response.status}`)
        }
        this.posts = await response.json()
      } catch (err) {
        this.error = err.message || 'Erreur réseau'
      } finally {
        this.loading = false
      }
    }
  },
  mounted() {
    this.loadPosts()
  }
}
</script>

<style scoped>
.api-container {
  margin: 100px auto 40px;
}
</style>