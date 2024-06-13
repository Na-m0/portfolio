<template>
    <div class="container-top">
        <h1 class="main-title">CONTEXTE</h1>
        <h1 class="overlay-title">CONTEXTE</h1>
        <div class="content">
            <div class="text">
                <p>
                    Lors de cette 2ème année au BUT Informatique, je devais faire ma première
                    découverte du monde du travail dans ce domaine. J’ai donc dû effectuer
                    mon premier stage afin d’en apprendre plus en milieu professionnel.
                    Ce premier stage à été effectué à la mairie de Montbéliard d’une
                    durée de 9 semaines, du 22 avril au 21 juin 2024.
                </p>
                <br>
                <p>
                    Le sujet de mon stage était “Création d'une application web de gestion de demandes informatiques en vue de la préparation budgétaire”. 
                    Cette application devait être créée de zéro avec des langages et des frameworks modernes.
                    Je n’avais pas de mission chaque semaine, mais un projet à réaliser seul, sans autres développeurs. Je devais donc voir les obligations 
                    des utilisateurs et faire en fonction de leur besoins.
                </p>
                <br>
                <p>
                    Le projet a pour objectif de garantir que les demandes parviennent jusqu'au maire de la ville pour être officiellement acceptées ou rejetées, 
                    en fonction des contraintes budgétaires de l'année.
                </p>
            </div>
            <div class="image">
                <img src="../assets/bureau.jpg" alt="Image descriptive" class="main-image">
                <!--<img src="../assets/pngegg.png" alt="Overlay Image" class="overlay-image">-->
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
            const contactSection = document.getElementById('langage');
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
    min-height: 100vh;
    position: relative;
}

h1.main-title {
    color: #CCC5B9;
    text-align: center;
    margin-bottom: 5%;
    position: relative;
    z-index: 2;
}

h1.overlay-title {
    position: absolute;
    top: 100px;
    left: 50%;
    transform: translate(-50%, 10px);
    font-size: 41px;
    color: rgba(255, 252, 242, 0.16);
    z-index: 1;
}

.content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-left: 10%;
    padding-right: 10%;
    padding-bottom: 10%;
}

.text {
    color: #CCC5B9;
    flex: 1;
}

.text p {
    word-spacing: 5px;
    font-size: 100%;
}

.image {
    flex: 1;
    position: relative;
    text-align: right;
}

.main-image {
    max-width: 80%;
    height: auto;
    border-radius: 15px;
}

.overlay-image {
    position: absolute;
    top: 62%;
    left: 50%;
    max-width: 80%;
    border-radius: 15px;
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
