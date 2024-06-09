<template>
    <div class="home" id="home">
        <div class="overlay"></div>
        <div class="t">
            <h1 class="titre">Portfolio de <span class="highlight">Noam </span>Joly-Girods</h1>
            <div class="underline"></div>
            <h2 class="sous-titre">Gestion de demandes informatiques à la mairie de Montbéliard</h2>
        </div>
        <div class="scroll-down" id="scrollDown" @click="handleContactClick">
          <a href="#next-section">
            <i class="fas fa-chevron-down"></i>
          </a>
        </div>
    </div>
</template>

<script>
export default {
  methods: {
      handleContactClick(event) {
          event.preventDefault(); // Empêche le comportement par défaut du clic sur le lien
          // Récupérez l'élément en bas de la page d'accueil
          const contactSection = document.getElementById('contexte');
          // Faites défiler la page jusqu'à cet élément
          if (contactSection) {
              contactSection.scrollIntoView({ behavior: 'smooth' });
          }
      },
  }
};
</script>

<style scoped>
.scroll-down {
  position: absolute;
  bottom: 60px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 1;
}

.scroll-down a {
  color: #EB5E28;
  font-size: 40px;
  text-decoration: none;
}

.scroll-down a:hover {
  color: #eb5f28da;
}

/* Transition de la flèche */
.scroll-down i {
  transition: transform 0.5s ease-in-out;
}

.scroll-down:hover i {
  transform: translateY(10px); /* Décale la flèche vers le bas lorsqu'elle est survolée */
}

h1 {
    font-size: 43px;
    color: #CCC5B9;
}

/* Nouveau style pour le texte surligné */
.highlight {
  color: #EB5E28; /* Couleur de la flèche */
}

/* Style de la ligne */
.underline {
  width: 85%; /* Largeur de la ligne */
  height: 2px; /* Épaisseur de la ligne */
  background-color: #CCC5B9; /* Couleur de la ligne */
  margin-top: 10px; /* Marge supérieure */
}

.home {
    width: 100%;
    height: 100vh;
    background-image: url('../assets/Mairie_de_Montbéliard.jpg');
    background-size:cover;
    background-position: center;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
}

.overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: radial-gradient(circle, rgba(0, 0, 0, 0.8), rgba(0, 0, 0, 0.4) 0%, rgba(0, 0, 0, 0.8) 80%);
}

.t {
    display: flex;
    flex-direction: column;
    align-items: center;
    z-index: 1;
}

.sous-titre {
    color: #CCC5B9;
    margin-top: 8px;
    font-weight: normal
}
</style>
