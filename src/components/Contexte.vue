<template>
    <div class="container-top">
      <h1>CONTEXTE</h1>
        <p>
          Lors de cette 2ème année au BUT Informatique, je devais faire ma première
          découverte du monde du travail dans ce domaine. J’ai donc dû effectuer
          mon premier stage afin d’en apprendre plus en milieu professionnel.
          J'ai donc décidé d'effectuer mon stage à la mairie de Montbéliard d’une
          durée de 9 semaines, du 22 avril au 21 juin 2024.
        </p>
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
          const contactSection = document.getElementById('competence');
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
    background-color: #252422;
    height: 100vh;
  }
  
  h1 {
    color: #CCC5B9;
    text-align: center;
    margin-bottom: 125px;
  }
  
  p {
    color: #CCC5B9;
  }
  


  .scroll-down {
  position: absolute;
  bottom: 60px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 1;
}

.scroll-down a {
  color: #CCC5B9;
  font-size: 40px;
  text-decoration: none;
}

.scroll-down a:hover {
  color: #ccc5b9d0;
}

/* Transition de la flèche */
.scroll-down i {
  transition: transform 0.5s ease-in-out;
}

.scroll-down:hover i {
  transform: translateY(10px); /* Décale la flèche vers le bas lorsqu'elle est survolée */
}
  </style>
  