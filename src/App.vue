<script setup>
import { ref, onMounted } from 'vue'
import { useRouter, RouterView } from 'vue-router'
import Navbar from './components/Navbar.vue'
import Footer from './components/Footer.vue'

const isLoading = ref(true)
const router = useRouter()

router.beforeEach((to, from, next) => {
  isLoading.value = true
  next()
})

router.afterEach(() => {
  setTimeout(() => {
    isLoading.value = false
  }, 1200)
})

onMounted(() => {
  isLoading.value = false
})
</script>

<template>
  <header>
    <Navbar />
  </header>

  <div v-if="isLoading" class="page-loader">
    <div class="loader-icon"></div>
    <span>Chargement...</span>
  </div>

  <main>
    <transition name="fade" mode="out-in">
      <RouterView v-if="!isLoading" />
    </transition>
  </main>
  <Footer v-show="!isLoading" />
</template>

<style>
html, body {
  margin: 0;
  padding: 0;
}

main,
.router-view {
  padding-top: 72px;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.2s ease;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
.fade-enter-to, .fade-leave-from {
  opacity: 1;
}

.page-loader {
  position: fixed;
  top: 60px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 8px 14px;
  background: rgba(0, 0, 0, 0.75);
  color: white;
  border-radius: 999px;
  z-index: 2000;
  backdrop-filter: blur(5px);
}

.loader-icon {
  width: 18px;
  height: 18px;
  border: 3px solid rgba(255, 255, 255, 0.3);
  border-top-color: #fff;
  border-radius: 50%;
  animation: spin 0.9s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}
</style>
