<template>
    <div class="container-top">
        <h1 class="main-title">TECHNOLOGIES</h1>
        <h1 class="overlay-title">TECHNOLOGIES</h1>
        <p class="text">Voici donc toutes les technologies utilisés afin de réussir ce projet.</p>
        <div class="allbook">
            <div class="book">
                <p class="texte">JavaScript est un langage de programmation de scripts principalement employé dans les pages web interactives et à ce 
                    titre est une partie essentielle des applications web.</p>
                <div class="cover js">
                    <img src="/src/assets/JavaScript.png" alt="Javascript">
                    <h2>JavaScript</h2>
                </div>
            </div>
            <div class="book">
                <p class="texte">Node.js est une plateforme open-source qui permet d'exécuter du code JavaScript côté serveur. Cela va permettre aux développeurs 
                    de construire des applications backend performantes</p>
                <div class="cover node">
                    <img src="/src/assets/NodeJS.png" alt="NodeJS">
                    <h2>Node.js</h2>
                </div>
            </div>
            <div class="book">
                <p class="texte">Vue.js, est un framework JavaScript open-source utilisé pour construire des interfaces utilisateur et des applications web monopages.</p>
                <div class="cover vue">
                    <img src="/src/assets/Vuejs.png" alt="VueJs">
                    <h2>Vue.js</h2>
                </div>
            </div>
            <div class="book">
                <p class="texte">PostgreSQL est un système de gestion de base de données relationnelle et objet.</p>
                <div class="cover post">
                    <img src="/src/assets/Postgresql.png" alt="PostgreSQL">
                    <h2>PostgreSQL</h2>
                </div>
            </div>
            <div class="book">
                <p class="texte">Figma est le principal outil de design collaboratif pour la création de produits significatifs.</p>
                <div class="cover figma">
                    <img src="/src/assets/Figma.svg" alt="Figma">
                    <h2>Figma</h2>
                </div>
            </div>
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
p.text {
    text-align: center;
    color: #252422;
    margin-bottom: 5%;
}

.texte {
    color: #FFFCF2;
    font-size: 14px;
    text-align: center;
    padding: 10px;
    margin-left: 25px;
}

.allbook {
    display: flex;
    justify-content: space-evenly;
}

.book {
  position: relative;
  border-radius: 10px;
  width: 220px;
  height: 300px;
  background-color: #252422;
  box-shadow: 1px 1px 12px #252422;
  transform: preserve-3d;
  perspective: 2000px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #252422;
}

.cover.vue {
    box-shadow: 1px 1px 12px #97d88a;
    background-color: rgb(160, 248, 189);
}
.cover.js {
    box-shadow: 1px 1px 12px #f4fd75;
    background-color: rgb(247, 248, 160);
}
.cover.node {
    box-shadow: 1px 1px 12px #7dc96e;
    background-color: rgb(216, 255, 200);
}
.cover.post {
    box-shadow: 1px 1px 12px #2585c5;
    background-color: rgb(160, 216, 248);
}
.cover.figma {
    box-shadow: 1px 1px 12px #c57225;
    background-color: rgb(248, 178, 160);
}


.cover {
  top: 0;
  position: absolute;
  width: 100%;
  height: 100%;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.5s;
  transform-origin: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.cover img {
  max-width: 80%; /* Ajuste la taille de l'image à votre convenance */
  max-height: 40%;
  display: block;
  border-radius: 10px;
  margin: 0 auto; /* Centre l'image horizontalement */
  margin-bottom: 15px; /* Espace entre l'image et le texte */
}

.book:hover .cover {
  transition: all 0.5s;
  transform: rotateY(-80deg);
}

h2 {
  font-size: 20px;
  font-weight: bolder;
}

/* Tout le container*/

.container-top {
    padding-top: 125px;
    background-color: #FFFCF2;
    height: 100vh;
    position: relative;
}

h1.main-title {
    color: #252422;
    text-align: center;
    margin-bottom: 3%;
    position: relative;
    z-index: 2;
}

h1.overlay-title {
    position: absolute;
    top: 100px;
    left: 50%;
    transform: translate(-50%, 10px);
    font-size: 41px;
    color: rgba(37, 36, 34, 0.14);
    z-index: 1;
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
    color: #252422;
}

/* Transition de la flèche */
.scroll-down i {
    transition: transform 0.5s ease-in-out;
}

.scroll-down:hover i {
    transform: translateY(10px); /* Décale la flèche vers le bas lorsqu'elle est survolée */
}
</style>
