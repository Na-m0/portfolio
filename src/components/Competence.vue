<template>
    <div class="container-top">
        <h1 class="main-title">COMPÉTENCES</h1>
        <h1 class="overlay-title">COMPÉTENCES</h1>
        <p class="text">Voici les compétences qui doivent être validées lors de la deuxième année de BUT Informatique.</p>
        <div class="cards-container">
            <div class="card"> <!-- Card de gauche -->
                <div class="card-header">
                    <div class="icon-circle">
                        <i class="icon fas fa-laptop-code"></i>
                    </div>
                    <h2>COMPÉTENCE 1</h2>
                    <p class="sous-text">Cette compétence consiste à transformer les besoins des clients en solutions informatiques concrètes. Cela passe par la conception, 
                        le codage, les tests et l'intégration des applications, tout en veillant à la qualité et à la documentation du code. Le développeur doit être capable de 
                        créer des applications, de les améliorer et de les maintenir en état de fonctionnement. Il doit également s'assurer que les interfaces utilisateur 
                        sont faciles à utiliser et accessibles, et que les applications répondent aux attentes grâce à des tests rigoureux.</p>
                </div>
                <a @click="openArbitrateDialog('COMPÉTENCE 1', 'icon fas fa-laptop-code', niveau1ListCompetence1, niveau2ListCompetence1)" class="voir-plus">Voir plus</a>
            </div>
            <div class="card"> <!-- Card de droite -->
                <div class="card-header">
                    <div class="icon-circle">
                        <i class="icon fas fa-database"></i>
                    </div>
                    <h2>COMPÉTENCE 4</h2>
                    <p class="sous-text">
                        Cette compétence consiste à concevoir, gérer, administrer et exploiter les bases de données de l'entreprise pour fournir les informations 
                        nécessaires à une gestion efficace. Elle inclut le respect des réglementations sur la protection des données personnelles et la prise en compte 
                        des enjeux économiques, sociétaux et écologiques. Le développement des bases de données doit suivre un cahier des charges précis, permettant des 
                        mises à jour, des requêtes et des visualisations efficaces, tout en optimisant les modèles de données et en assurant leur sécurité et confidentialité.</p>
                </div>
                <a @click="openArbitrateDialog('COMPÉTENCE 4', 'icon fas fa-database', niveau1ListCompetence4, niveau2ListCompetence4)" class="voir-plus">Voir plus</a>
            </div>
        </div>
        <div class="scroll-down" id="scrollDown" @click="handleContactClick">
            <a href="#next-section">
                <i class="fas fa-chevron-down"></i>
            </a>
        </div>
        <div v-if="showDialog" class="modal">
            <div class="modal-content">
                <span class="close" @click="closeDialog">&times;</span>
                <div class="arbitrage">
                    <div class="icon-circle">
                        <i :class="currentIcon"></i>
                    </div>
                    <h2>{{ currentTitle }}</h2>
                    <div class="text-container">
                        <div class="text-section">
                            <h3>Niveau 1</h3>
                            <ul>
                                <li v-for="item in currentDescriptionList1" :key="item">{{ item }}</li>
                            </ul>
                        </div>
                        <div class="text-section">
                            <h3>Niveau 2</h3>
                            <ul>
                                <li v-for="item in currentDescriptionList2" :key="item">{{ item }}</li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            showDialog: false,
            currentTitle: '',
            currentIcon: '',
            currentDescriptionList1: [],
            currentDescriptionList2: [],
            // Exemples de listes pour les compétences
            niveau1ListCompetence1: [
                'AC 1 Implémenter des conceptions simples',
                'AC 2 Élaborer des conceptions simples',
                'AC 3 Faire des essais et évaluer leurs résultats en regard des spécifications',
                'AC 4 Développer des interfaces utilisateurs'],
            niveau2ListCompetence1: [
                'AC 1 Élaborer et implémenter les spécifications fonctionnelles et non fonctionnelles à partir des exigences',
                'AC 2 Appliquer des principes d’accessibilité et d’ergonomie',
                'AC 3 Adopter de bonnes pratiques de conception et de programmation',
                'AC 4 Vérifier et valider la qualité de l’application par les tests'],
            niveau1ListCompetence4: [
                'AC 1 Mettre à jour et interroger une base de données relationnelle (en requêtes directes ou à travers une application)',
                'AC 2 Visualiser des données',
                'AC 3 Concevoir une base de données relationnelle à partir d’un cahier des charges'],
            niveau2ListCompetence4: [
                'AC 1 Optimiser les modèles de données de l’entreprise',
                'AC 2 Assurer la confidentialité des données (intégrité et sécurité)',
                'AC 3 Organiser la restitution de données à travers la programmation et la visualisation',
                'AC 4 Manipuler des données hétérogènes'],
        }
    },
    methods: {
        openArbitrateDialog(title, icon, descriptionList1, descriptionList2) {
            this.currentTitle = title;
            this.currentIcon = icon;
            this.currentDescriptionList1 = descriptionList1;
            this.currentDescriptionList2 = descriptionList2;
            this.showDialog = true;
        },
        closeDialog() {
            this.showDialog = false;
        },
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
.arbitrage {
    display: flex;
    flex-direction: column;
    align-items: center;
}

/* Styles pour la modale */
.modal {
    display: flex;
    justify-content: center;
    align-items: center;
    position: fixed;
    z-index: 3;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: auto;
    background-color: rgba(0, 0, 0, 0.4);
}

.modal-content {
    position: relative;
    background-color: #fff;
    margin: auto;
    padding: 20px;
    border: 1px solid #888;
    width: 50%;
    height: 70%;
    border-radius: 5px;
    text-align: center;
    align-content: center;
}

.close {
    position: absolute;
    top: 10px;
    right: 15px;
    color: #aaa;
    font-size: 28px;
    font-weight: bold;
}

.close:hover,
.close:focus {
    color: black;
    text-decoration: none;
    cursor: pointer;
}

.card-header {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.icon-circle {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 80px;
    height: 80px;
    background-color: rgba(235, 94, 40, 0.35);
    border-radius: 50%;
    margin-bottom: 30px;
}

.icon {
    color: #EB5E28;
    font-size: 40px;
}

.text-container {
    display: flex;
    justify-content: space-between;
    width: 100%;
    padding: 0 20px;
}

.text-section {
    width: 45%;
    text-align: left;
}

.text-section li {
    margin-bottom: 10px; /* Ajustez cette valeur pour l'espacement souhaité */
}

.text-section h3 {
    text-align: center;
    color: #252422;
    margin-bottom: 20px; /* Ajustez cette valeur pour l'espacement souhaité */
    margin-top: 20px; /* Ajout d'une marge en haut si nécessaire */
}

.text-section ul {
    list-style-type: disc;
    margin-left: 20px;
    color: #252422;
}

.text-section p {
    text-align: center;
    color: #252422;
}

/* Card */
.container-top {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding-top: 125px;
    background-color: #CCC5B9;
    height: 100vh;
    position: relative;
}

h1.main-title {
    color: #252422;
    text-align: center;
    margin-bottom: 30px;
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

h2 {
    color: #252422;
    margin-bottom: 20px;
}

p.text {
    text-align: center;
    font-size: 1.2vw;
    color: #252422;
    margin-bottom: 30px;
}

.sous-text {
    text-align: center;
    color: #252422;
    margin-right: 5%;
    margin-left: 5%;
    font-size: 1.2vw; /* Taille de la police en fonction de la largeur de l'écran */
}

.cards-container {
    display: flex;
    justify-content: space-between;
    margin-bottom: 8%;
    padding: 0 5%;
    flex-grow: 1;
    align-items: stretch;
}

.card {
    border-radius: 10px;
    background-color: #FFFCF2;
    padding: 20px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.4);
    width: calc(45% - 10px);
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    position: relative;
}

.voir-plus {
    cursor: pointer;
    text-align: right;
    color: #787878;
    text-decoration: none;
    font-weight: normal;
}

.voir-plus:hover {
    text-decoration: underline;
}

.scroll-down {
    position: absolute;
    bottom: 60px;
    text-align-last: center;
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
