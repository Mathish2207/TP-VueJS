<template>
  <nav class="navbar">
    <div class="navbar-container">
      <div class="navbar-logo">MyApp</div>
      <button class="burger" @click="toggleMenu" aria-label="Toggle navigation">
        <span></span>
        <span></span>
        <span></span>
      </button>
      <ul :class="['nav-menu', { 'active': isOpen }]">
        <li class="nav-item">
          <RouterLink class="nav-link" to="/">Home</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink class="nav-link" to="/about">About</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink class="nav-link" to="/contact">Contact</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink class="nav-link" to="/qcm">QCM</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink class="nav-link" to="/api">API REST</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink class="nav-link" to="/localisation">Localisation</RouterLink>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Navbar',
  data() {
    return {
      isOpen: false,
    };
  },
  methods: {
    toggleMenu() {
      this.isOpen = !this.isOpen;
    },
  },
};
</script>

<style scoped>
.navbar {
  background-color: #333;
  padding: 1rem 0;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  width: 100%;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  z-index: 1000;
}

.navbar-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.navbar-logo {
  font-size: 1.5rem;
  font-weight: bold;
  color: #fff;
}

.burger {
  display: none;
  flex-direction: column;
  justify-content: space-between;
  width: 24px;
  height: 18px;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 0;
}

.burger span {
  display: block;
  height: 2px;
  width: 100%;
  background-color: #fff;
}

.nav-menu {
  display: flex;
  list-style: none;
  gap: 2rem;
  margin: 0;
  padding: 0;
}

.nav-item {
  margin: 0;
}

.nav-link {
  color: #fff;
  text-decoration: none;
  font-size: 1rem;
  transition: color 0.3s ease;
}

.nav-link:hover {
  color: #4CAF50;
}

@media (max-width: 768px) {
  .burger {
    display: flex;
  }

  .nav-menu {
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    background-color: #333;
    flex-direction: column;
    gap: 0;
    overflow: hidden;
    max-height: 0;
    transition: max-height 0.3s ease;
  }

  .nav-menu.active {
    max-height: 500px;
  }

  .nav-item {
    padding: 0.75rem 1.5rem;
  }

  .nav-link {
    display: block;
  }

  .navbar-container {
    padding: 0 1rem;
  }
}
</style>