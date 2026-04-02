<template>
  <footer class="footer">
    <div class="footer-content">
      <div class="footer-section">
        <h3>À propos</h3>
        <p>Informations sur l'entreprise.</p>
      </div>
      <div class="footer-section">
        <h3>Liens utiles</h3>
        <ul>
          <li><RouterLink to="/contact">Contact</RouterLink></li>
          <li><RouterLink to="/mentions">Mentions légales</RouterLink></li>
          <li><RouterLink to="/privacy">Politique de confidentialité</RouterLink></li>
        </ul>
      </div>
      <div class="footer-section">
        <h3>Suivez-nous</h3>
        <ul>
          <li><a href="#">Facebook</a></li>
          <li><a href="#">Twitter</a></li>
          <li><a href="#">LinkedIn</a></li>
        </ul>
      </div>
    </div>
    <div class="footer-bottom">
      <p>&copy; 2026 Tous droits réservés.</p>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'Footer'
}
</script>

<style scoped>
.footer {
  background-color: #333;
  color: #fff;
  padding: 40px 20px 20px;
  margin: 0;
  border-top: 1px solid #555;
  width: 100vw;
  position: relative;
  left: 50%;
  right: 50%;
  margin-left: -50vw;
  margin-right: -50vw;
  margin-top: 30px;
}

.footer-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 30px;
  max-width: 1200px;
  margin: 0 auto 30px;
}

.footer-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 30px;
  max-width: 1200px;
  margin: 0 auto 30px;
}

.footer-section h3 {
  margin-bottom: 15px;
  font-size: 18px;
}

.footer-section ul {
  list-style: none;
  padding: 0;
}

.footer-section ul li {
  margin-bottom: 8px;
}

.footer-section a {
  color: #ccc;
  text-decoration: none;
  transition: color 0.3s ease;
}

.footer-section a:hover {
  color: #fff;
}

.footer-bottom {
  text-align: center;
  border-top: 1px solid #555;
  padding-top: 20px;
  font-size: 14px;
  color: #999;
}
</style> 