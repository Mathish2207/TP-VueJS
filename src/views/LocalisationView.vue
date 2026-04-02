<template>
  <v-container class="localisation-container" max-width="960">
    <v-card elevation="2" class="pa-6">
      <v-card-title class="text-h5 justify-center">Localisation</v-card-title>

      <div class="d-flex justify-space-between align-center mb-4">
        <v-btn color="primary" @click="requestLocation" :loading="loading" outlined>
          Récupérer ma position
        </v-btn>
        <div>{{ locationStatus }}</div>
      </div>

      <div v-if="hasLocation" class="map-wrapper">
        <iframe
          :src="mapSrc"
          width="100%"
          height="450"
          frameborder="0"
          style="border:0"
          allowfullscreen=""
          aria-hidden="false"
          tabindex="0"
        ></iframe>
      </div>

      <v-alert v-else type="info" border="left" colored-border>
        Clique sur "Récupérer ma position" pour afficher votre emplacement sur la carte.
      </v-alert>

      <v-card-text class="mt-4" v-if="hasLocation">
        <p><strong>Latitude :</strong> {{ latitude.toFixed(6) }}</p>
        <p><strong>Longitude :</strong> {{ longitude.toFixed(6) }}</p>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script>
export default {
  name: 'LocalisationView',
  data() {
    return {
      latitude: null,
      longitude: null,
      loading: false,
      locationStatus: 'Prêt'
    }
  },
  computed: {
    hasLocation() {
      return this.latitude !== null && this.longitude !== null
    },
    mapSrc() {
      if (!this.hasLocation) return ''
      const base = 'https://www.openstreetmap.org/export/embed.html'
      const zoom = 15
      const bbox = `${this.longitude - 0.01},${this.latitude - 0.01},${this.longitude + 0.01},${this.latitude + 0.01}`
      const marker = `marker=${this.latitude},${this.longitude}`
      return `${base}?bbox=${bbox}&layer=mapnik&${marker}`
    }
  },
  methods: {
    requestLocation() {
      if (!navigator.geolocation) {
        this.locationStatus = 'Géolocalisation non supportée.'
        return
      }

      this.loading = true
      this.locationStatus = 'Récupération en cours...'

      navigator.geolocation.getCurrentPosition(
        (position) => {
          this.latitude = position.coords.latitude
          this.longitude = position.coords.longitude
          this.locationStatus = 'Localisation trouvée'
          this.loading = false
        },
        (error) => {
          this.loading = false
          switch (error.code) {
            case error.PERMISSION_DENIED:
              this.locationStatus = 'Autorisation refusée.'
              break
            case error.POSITION_UNAVAILABLE:
              this.locationStatus = 'Position indisponible.'
              break
            case error.TIMEOUT:
              this.locationStatus = 'Délai dépassé.'
              break
            default:
              this.locationStatus = 'Erreur de localisation.'
          }
        },
        {
          enableHighAccuracy: true,
          timeout: 15000,
          maximumAge: 0
        }
      )
    }
  }
}
</script>

<style scoped>
.localisation-container {
  margin: 100px auto 40px;
}

.map-wrapper {
  min-height: 450px;
  margin-bottom: 16px;
  border: 1px solid #ccc;
  border-radius: 8px;
  overflow: hidden;
}
</style>