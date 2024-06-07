<template>
    <div class="container-top">
        <h1>Compétences</h1>
        <p>Voici les compétences qui doivent être validées lors de la deuxième année de BUT Informatique.</p>
        <div class="images-container">
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
          const contactSection = document.getElementById('projet');
          // Faites défiler la page jusqu'à cet élément
          if (contactSection) {
              contactSection.scrollIntoView({ behavior: 'smooth' });
          }
      },
  }
};
</script>

<style scoped>
.container-top {
    padding-top: 125px;
    background-color: #CCC5B9;
    height: 100vh;
}

h1 {
    text-align: center;
    margin-bottom: 125px;
    color: #252422;
}



.scroll-down {
  position: absolute;
  bottom: 60px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 1;
}

.scroll-down a {
  color: #252422;
  font-size: 40px;
  text-decoration: none;
}

.scroll-down a:hover {
  color: #252422c7;
}

/* Transition de la flèche */
.scroll-down i {
  transition: transform 0.5s ease-in-out;
}

.scroll-down:hover i {
  transform: translateY(10px); /* Décale la flèche vers le bas lorsqu'elle est survolée */
}


</style>
