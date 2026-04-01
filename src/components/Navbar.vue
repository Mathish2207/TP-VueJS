<template>
  <nav class="navbar">
    <div class="navbar-container">
      <div class="navbar-logo">MyApp</div>
      <ul class="nav-menu">
        <li class="nav-item">
            <RouterLink to="/">Home</RouterLink>
        </li>
        <li class="nav-item">
            <RouterLink to="/about">About</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink to="/contact">Contact</RouterLink>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Navbar'
}
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
</style>