<template>
    <div class="container-top">
      <h1 class="main-title">PROJET</h1>
      <h1 class="overlay-title">PROJET</h1>
      <p class="sous-titre">Voici donc les différentes étapes du projet qui m'ont permis de valider les apprentissages critiques des compétences présentées.</p>
      <div class="swiper-container slideshow">
        <div class="swiper-wrapper">
          <div class="swiper-slide slide" v-for="(slide, index) in slides" :key="index">
            <div class="slide-card">
              <div class="text-content">
                <h2 class="slide-title">{{ slide.title }}</h2>
                <p class="slide-text">{{ slide.text }}</p>
                <h3 class="slide-subtitle">Apprentissage(s) critique(s) validé(s)</h3>
                <div class="learning-container">
                  <!-- Affichage des compétences -->
                  <div v-for="competence in slide.competences" :key="competence.name" class="competence-block">
                    <h3>{{ competence.name }}</h3>
                    <div v-for="level in competence.levels" :key="level.level" class="level">
                      <h4>{{ level.level }}</h4>
                      <div class="ac-group" v-if="level.acs.length > 1">
                        <div class="circle" v-for="ac in level.acs" :key="ac"><p>{{ ac }}</p></div>
                      </div>
                      <div class="circle" v-else><p>{{ level.acs[0] }}</p></div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="image-content image-container">
                <img :src="slide.images[0]" alt="Slide image" class="slide-image" @click="openImage(slide.images, 0)"/>
                <div class="image-indicators">
                  <div v-for="(image, imgIndex) in slide.images" :key="imgIndex" @click="goToImage(index, imgIndex)" :class="{ active: imgIndex === currentImageIndex }" class="indicator"></div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="slideshow-navigation">
          <div class="slideshow-navigation-button prev slideshow-navigation-button-L" @click="prevSlide">
            <i class="fas fa-chevron-left"></i>
          </div>
          <div class="slideshow-navigation-button next slideshow-navigation-button-R" @click="nextSlide">
            <i class="fas fa-chevron-right"></i>
          </div>
        </div>
      </div>
      <div class="slideshow-progress">
        <div class="progress-bar" :style="{ width: progress + '%' }"></div>
      </div>

      <!-- Modal pour l'affichage plein écran des images -->
      <div v-if="fullscreenImage" class="fullscreen-image-modal">
        <button class="close-button" @click="closeImage">✖</button>
        <button @click="prevModalImage" class="modal-nav-button left"><i class="fas fa-chevron-left"></i></button>
        <img :src="fullscreenImage" alt="Fullscreen image"/>
        <button @click="nextModalImage" class="modal-nav-button right"><i class="fas fa-chevron-right"></i></button>
        <div class="image-indicators">
          <div v-for="(image, imgIndex) in modalImages" :key="imgIndex" @click="setCurrentImageIndex(imgIndex)" :class="{ active: imgIndex === currentImageIndex }" class="indicator"></div>
        </div>
      </div>
    </div>
  </template>
  
  
<script>
import { onMounted, ref } from 'vue';
import Swiper from 'swiper';
import 'swiper/swiper-bundle.css';
import charming from 'charming';
import { TweenMax, Back, Expo, Quart } from 'gsap';
import image1 from '../assets/projet/photo/plan.jpg';
import image2 from '../assets/projet/photo/plan2.jpg';
import image3 from '../assets/projet/photo/schema1.jpg';
import image4 from '../assets/projet/photo/schema2.jpg';
import image5 from '../assets/projet/photo/schema3.jpg';

import image6 from '../assets/projet/photo/exemple_table.jpg';
import image7 from '../assets/projet/screen/premier_mcd_créé.png';

import image8 from '../assets/projet/screen/deuxième_mcd_avec_modif_agent.png';

import image10 from '../assets/Postgresql.png';
import image11 from '../assets/projet/screen/API_1.png';
import image12 from '../assets/projet/screen/requete.jpg';

import image13 from '../assets/projet/screen/all_figma.png';
import image14 from '../assets/projet/screen/home_figma.png';

import image15 from '../assets/projet/screen/vue_dossier1.png';
import image52 from '../assets/projet/screen/login_debut.png';
import image53 from '../assets/projet/code/login.png';
import image54 from '../assets/projet/code/data_login.png';
import image55 from '../assets/projet/code/login_submit.png';
import image56 from '../assets/projet/screen/home_debut.png';

import image16 from '../assets/projet/screen/token_exemple.png';
import image17 from '../assets/projet/code/generer_token.png';
import image18 from '../assets/projet/code/token_exemple.png';

import image57 from '../assets/projet/screen/home2_vue.png';
import image58 from '../assets/projet/screen/demande_vue_1.png';
import image59 from '../assets/projet/code/demande_vue.png';
import image19 from '../assets/projet/code/demandes_service.png';

import image20 from '../assets/projet/screen/accueil_vue.png';
import image21 from '../assets/projet/screen/demandes_vue.png';

import image22 from '../assets/projet/screen/accueil_vue_2.png';

import image23 from '../assets/projet/code/demandes_service.png';
import image24 from '../assets/projet/code/statut.png';
import image25 from '../assets/projet/code/statut_script.png';
import image26 from '../assets/projet/code/budget.png';

import image31 from '../assets/projet/screen/boutton_vue.png';
import image27 from '../assets/projet/screen/modifier_demande_vue.png';
import image28 from '../assets/projet/code/modif_demande.png';
import image29 from '../assets/projet/screen/ajout_demande_vue.png';
import image30 from '../assets/projet/code/ajout_demande.png';

import image32 from '../assets/projet/screen/dg_services_vue.png';
import image33 from '../assets/projet/code/data_fonction.png';
import image34 from '../assets/projet/code/service_dg.png';
import image35 from '../assets/projet/code/services_dg.png';

import image36 from '../assets/projet/screen/arbitrage_vue.png';
import image37 from '../assets/projet/screen/arbitrage_fenettre_vue.png';
import image38 from '../assets/projet/code/insert_statut.png';
import image39 from '../assets/projet/code/modif_statut_service.png';
import image40 from '../assets/projet/code/submit_fenettre.png';
import image41 from '../assets/projet/code/submit_fonction.png';
import image42 from '../assets/projet/code/statut_couleur.png';

import image43 from '../assets/projet/screen/troisième_mcd_avec_pj.png';
import image44 from '../assets/projet/screen/ajout_fichier_avant.png';
import image45 from '../assets/projet/screen/ajout_fichier_test.png';
import image46 from '../assets/projet/screen/dossier_upload.png';

import image51 from '../assets/projet/screen/upload_fichier_id.png';


import image47 from '../assets/projet/screen/motif_arbitrage_vue.png';
import image48 from '../assets/projet/screen/motif_demande.png';
import image49 from '../assets/projet/code/ajout_motif.png';
import image50 from '../assets/projet/code/motif_ajout.png';

export default {
    mounted() {
      window.addEventListener('keydown', this.keydownHandler);
    },
    beforeUnmount() {
      window.removeEventListener('keydown', this.keydownHandler);
    },
    methods: {
      keydownHandler(event) {
        switch (event.key) {
          case 'ArrowLeft':
            this.prevSlide();
            break;
          case 'ArrowRight':
            this.nextSlide();
            break;
          default:
            return;
        }
        this.updateProgress();
      },
    },
    setup() {
    const slides = ref([
           {
               title: `Étape 1 : Analyse du cahier des charges`,
               text: `Au début de mon stage, on m'a confié le cahier des charges du projet. J'ai analysé les exigences de celui-ci pour comprendre 
               les objectifs et les contraintes du projet. J’ai pu réfléchir à des schémas afin d’avoir une visualisation de la gestion de 
               l’application et de tous ses besoins. Par exemple, j'ai dû comprendre comment fonctionnait la hiérarchie des agents de la mairie 
               et quels étaient les services présents. J'ai donc élaboré une conception simple du projet à l'aide de ces schémas.`,
               images: [image1,image2,image3,image4,image5], // Liste des images pour cette slide
               competences: [
                   {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 2 | Élaborer des conceptions simples'] },
                       ]
                   },
               ]
           },
           {
               title:`Étape 2 : Réflexion et conception du modèle de données`,
               text: `Suite au schéma que j'ai effectué, j'ai commencé à réfléchir au modèle de données de l'application. J'ai donc imaginé dans un 
               premier temps les différentes tables qui pourraient exister pour le projet. J’ai pu concevoir un premier Modèle Conceptuel des Données (MCD) avec les données
               écrites dans le cahier des charges, telles que les agents, les demandes ou encore les fonctions des agents. Comme il doit y avoir une hiérarchie, 
               j'ai imaginé des tables des directeurs au-dessus des agents, mais comme je vais le montrer plus tard, cela posera un problème.`,
               images: [image6, image7],
               competences: [
                   {
                       name: 'Compétence 4',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 3 | Concevoir une base de données relationnelle à partir d’un cahier des charges'] },
                       ]
                   },
               ]
           },
           {
               title: 'Étape 3 : Création de la base de données (BDD)',
               text: `Afin de créer la base de données, j'ai décidé d'utiliser PostgreSQL, qui permet de créer les tables et de faire la 
               simulation des jeux de données. Pour la gestion de ces données, j'ai conçu une API Rest qui permettra d'afficher, d'ajouter, 
               de modifier ou de supprimer les données dans la vue de l'application. J'ai donc créé les premières requêtes de chaque table dans 
               l'API en respectant les bonnes pratiques de conception et de programmation, c'est-à-dire en créant les dossiers controllers, 
               routes et services, et en créant un fichier par table.`,
               images: [image10, image12, image11],
               competences: [
                    {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 2', acs: ['AC 3 | Adopter de bonnes pratiques de conception et de programmation'] },
                       ]
                   },
                   {
                       name: 'Compétence 4',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 1 | Mettre à jour et interroger une base de données relationnelle (en requêtes directes ou à travers une application)',
                                                      'AC 3 | Concevoir une base de données relationnelle à partir d’un cahier des charges'] },
                       ]
                   },
               ]
           },
           {
               title: 'Étape 4 : Création de la maquette du site',
               text: `Pour y voir plus clair sur l’application et ne pas avancer au hasard, j’ai décidé de créer sur Figma, une maquette des pages principales pour les 
               utilisateurs. Cela m’a aidé à développer les pages plus facilement et m'a également permis d’arranger les différents modules de l’application
               de la manière la plus ergonomique possible.`,
               images: [image14,image13],
               competences: [
                   {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 2 | Élaborer des conceptions simples'] },
                           { level: 'Niveau 2', acs: ['AC 2 | Appliquer des principes d’accessibilité et d’ergonomie'] },
                       ]
                   },
               ]
           },
           {
               title: `Étape 5 : Développement de l'interface utilisateur avec Vue.js`,
               text: `Le backend étant conçu et les maquettes créées, j'ai donc commencé à développer le frontend de l'application avec Vue.js. 
               Après avoir créé la vue de l'application, j'ai commencé à développer une première page de connexion avec des champs permettant à 
               l'utilisateur de se connecter via des requêtes envoyées à l'API qui vérifie si l'utilisateur existe. J'ai respecté les bonnes pratiques de 
               conception et de programmation, c'est-à-dire en créant les dossiers "router" pour la liaison des pages, "components" et "views" 
               pour une structuration claire des pages, et "store" pour la réutilisation des fonctions qui font appel à l'API. J'ai donc élaboré une 
               conception simple de la connexion avec des requêtes vers l'API.`,
               images: [image15, image52, image53, image54, image55, image56],
               competences: [
                   {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 1 | Implémenter des conceptions simples',
                                                      'AC 4 | Développer des interfaces utilisateurs'] },
                           { level: 'Niveau 2', acs: ['AC 3 | Adopter de bonnes pratiques de conception et de programmation'] },
                       ]
                   },
                   {
                        name: 'Compétence 4',
                        levels: [
                            { level: 'Niveau 1', acs: ['AC 1 | Mettre à jour et interroger une base de données relationnelle (en requêtes directes ou à travers une application)'] },
                        ]
                    },
               ]
           },
           {
                title: `Étape 6 : Implémentation de la gestion des tokens des utilisateurs`,
                text: `Pour compléter la connexion, j’ai élaboré une fonction de gestion des tokens lors de l’identification.
                Au moment de sa création, ce token est séparé en trois grands blocs : le "header", le "payload" et la "signature". Grâce à ce token, les utilisateurs
                peuvent être gérés et bénéficier de certains droits d'utilisation sur l'application. Tout cela est fait dans le "store", ce qui permet de réutiliser 
                les fonctions d'autorisation n'importe où dans l'application.`,
                images: [image16, image17, image18],
                competences: [
                    {
                        name: 'Compétence 1',
                        levels: [
                            { level: 'Niveau 2', acs: ['AC 1 | Élaborer et implémenter les spécifications fonctionnelles et non fonctionnelles à partir des exigences',
                                                      'AC 3 | Adopter de bonnes pratiques de conception et de programmation'] },
                        ]
                    },
                    {
                        name: 'Compétence 4',
                        levels: [
                            { level: 'Niveau 1', acs: ['AC 1 | Mettre à jour et interroger une base de données relationnelle (en requêtes directes ou à travers une application)'] },
                            { level: 'Niveau 2', acs: ['AC 2 | Assurer la confidentialité des données (intégrité et sécurité)'] },
                        ]
                    },
                ]
           },
           {
                title: `Étape 7 : Affichage des demandes du service lors de la connexion de l'utilisateur`,
                text: `Pour gérer les demandes, il faut d'abord les afficher. J'ai donc créé une requête qui 
                affiche les demandes du service auquel l’agent est relié. Ces requêtes permettent d’afficher toutes les données des demandes 
                dans la vue de l’application pour chaque agent relié à un service, afin qu'il puisse voir les demandes spécifiques à son service. 
                Il a également été nécessaire de créer d'autres requêtes pour récupérer les données d'autres tables liées à la demande, telles que 
                la propriété ou le type de demande. À l'aide de jeux de données, j'ai testé si la visualisation affichait correctement les bonnes données des demandes liées aux services.`,
                images: [image57,image58, image59,image19],
                competences: [
                    {
                        name: 'Compétence 1',
                        levels: [
                            { level: 'Niveau 1', acs: ['AC 3 | Faire des essais et évaluer leurs résultats en regard des spécifications'] },
                            { level: 'Niveau 2', acs: ['AC 1 | Élaborer et implémenter les spécifications fonctionnelles et non fonctionnelles à partir des exigences'] },
                        ]
                    },
                    {
                        name: 'Compétence 4',
                        levels: [
                            { level: 'Niveau 1', acs: ['AC 1 | Mettre à jour et interroger une base de données relationnelle (en requêtes directes ou à travers une application)',
                                                        'AC 2 | Visualiser des données'] },
                        ]
                    },
                ]
           },
           {
               title: `Étape 8 : Correction des problèmes liés au modèle de données`,
               text: `En voulant effectuer la connexion des agents avec une fonction supérieure, je me suis rendu compte que les tables des directeurs 
               généraux (DGA et DGS) n'étaient pas du tout utiles pour cette connexion, puisque la table "fonction" permettait aux agents d'obtenir ces rôles. 
               J’ai donc modifié le MCD afin de résoudre ces problèmes et d'avoir un modèle de données bien plus clair. Grâce à cette table "fonction", 
               il est donc possible de gérer les droits des utilisateurs. On pourra autoriser certaines actions de l'utilisateur uniquement s'ils possèdent la fonction requise.`,
               images: [image8],
               competences: [
                   {
                       name: 'Compétence 4',
                       levels: [
                           { level: 'Niveau 2', acs: ['AC 1 | Optimiser les modèles de données de l’entreprise',
                                   'AC 2 | Assurer la confidentialité des données (intégrité et sécurité)',
                                   'AC 3 | Organiser la restitution de données à travers la programmation et la visualisation'] },
                       ]
                   },
               ]
           },
           {
               title: `Étape 9 : Amélioration graphique de l'application`,
               text: `Afin de rendre l'application conforme au design sur Figma, j'ai refait tout le design de l'application. Cela m'a pris beaucoup de temps, 
               mais c'était très important pour l'expérience utilisateur. Il était essentiel que les personnes testant l'application puissent l'apprécier et
               la comprendre. Il fallait également adapter le design en fonction des retours des utilisateurs.`,
               images: [image20, image21],
               competences: [
                   {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 3 | Faire des essais et évaluer leurs résultats en regard des spécifications',
                                   'AC 4 | Développer des interfaces utilisateurs'] },
                           { level: 'Niveau 2', acs: ['AC 2 | Appliquer des principes d’accessibilité et d’ergonomie'] },
                       ]
                   }
               ]
           },
           {
               title: `Étape 10 : Ajout de fonctionnalités à la page d'accueil`,
               text: `Afin d’améliorer l'expérience utilisateur, j’ai décidé de rajouter des indications sur le ou les services qui sont reliés à l'utilisateur.
               J’ai donc ajouté des requêtes à l’API afin d’obtenir les données souhaitées, telles que le nombre de demandes, le budget total 
               des demandes et les différents statuts des demandes. Toutes les requêtes interrogent la base de données pour obtenir les informations 
               souhaitées, qui sont ensuite affichées dans la vue de l’utilisateur. J'ai également vérifié que les données récupérées étaient correctes 
               et qu'aucun bug n'intervenait.`,
               images: [image22, image26, image23, image24, image25],
               competences: [
                   {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 3 | Faire des essais et évaluer leurs résultats en regard des spécifications',
                                   'AC 4 | Développer des interfaces utilisateurs'] },
                           { level: 'Niveau 2', acs: ['AC 1 | Élaborer et implémenter les spécifications fonctionnelles et non fonctionnelles à partir des exigences'] },
                       ]
                   },
                   {
                       name: 'Compétence 4',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 1 | Mettre à jour et interroger une base de données relationnelle (en requêtes directes ou à travers une application)'] },
                       ]
                   },
               ]
           },
           {
               title: `Étape 11 : Développement des pages d'ajout et de modification de demandes`,
               text: `S'il y a des demandes, il doit être possible d’en ajouter et de les modifier. J’ai donc ajouté les pages 
               d’ajout et de modification des demandes, en prenant en compte les informations écrites dans le cahier des charges à 
               inclure lors de l’ajout et de la modification. Les données sont donc modifiées, ajoutées et visualisées grâce aux requêtes de l’API, 
               ce qui permet une gestion des demandes par les utilisateurs. J'ai également vérifié que les données sont bien ajoutées ou modifiées.`,
               images: [image31, image27, image28, image29, image30],
               competences: [
                   {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 3 | Faire des essais et évaluer leurs résultats en regard des spécifications'] },
                           { level: 'Niveau 2', acs: ['AC 1 | Élaborer et implémenter les spécifications fonctionnelles et non fonctionnelles à partir des exigences'] },
                       ]
                   },
                   {
                       name: 'Compétence 4',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 1 | Mettre à jour et interroger une base de données relationnelle (en requêtes directes ou à travers une application)'] },
                       ]
                   },
               ]
           },
           {
                title: `Étape 12 : Implémentation de la connexion d'un Directeur Général Adjoint`,
                text: `Dans cette application, il y a une hiérarchie des agents. Il faut donc, grâce aux fonctions ajoutées dans la table, 
                gérer qui aura certains droits dans la vue. J'ai analysé les exigences de la hiérarchie des agents et les ai traduites en spécifications fonctionnelles, 
                en mettant en place les différentes permissions pour les agents et les directeurs. J'ai conçu une interface pour les directeurs leur petettant de gérer les demandes de leurs services. J'ai testé les fonctionnalités pour m'assurer que
                les agents et les directeurs avaient bien les droits spécifiés.
                J'ai assuré la confidentialité et la sécurité des données en implémentant des contrôles d’accès stricts, garantissant que seuls les utilisateurs 
                autorisés pouvaient accéder et modifier les données des demandes.`,
                images: [image32, image33, image34, image35],
                competences: [
                    {
                        name: 'Compétence 1',
                        levels: [
                            { level: 'Niveau 1', acs: ['AC 3 | Faire des essais et évaluer leurs résultats en regard des spécifications',
                                    'AC 4 | Développer des interfaces utilisateurs'] },
                            { level: 'Niveau 2', acs: ['AC 1 | Élaborer et implémenter les spécifications fonctionnelles et non fonctionnelles à partir des exigences',
                                    'AC 2 | Appliquer des principes d’accessibilité et d’ergonomie'] },
                        ]
                    },
                    {
                        name: 'Compétence 4',
                        levels: [
                            { level: 'Niveau 1', acs: ['AC 1 | Mettre à jour et interroger une base de données relationnelle (en requêtes directes ou à travers une application)',
                                    'AC 2 | Visualiser des données'] },
                            { level: 'Niveau 2', acs: ['AC 2 | Assurer la confidentialité des données (intégrité et sécurité)'] },
                        ]
                    },
                ]
           },
           {
               title: `Étape 13 : Implémentation de la fonctionnalité d'arbitrage des demandes`,
               text: `Comme le but de l’application est d'arbitrer des demandes selon différentes hiérarchies, 
               j’ai élaboré le système d’arbitrage de la demande qui met à jour son statut lors de la validation ou du refus. 
               Cela change le stade de validation lorsque le compte d’un responsable ou d’un directeur arbitre la demande. Les utilisateurs en dessous des 
               directeurs ne pourront donc plus avoir accès à la modification ou à la suppression de la demande lorsque celle-ci sera arbitrée, ce qui assure 
               la sécurité de gestion des données selon la fonction des utilisateurs. J’ai aussi testé si les utilisateurs avec une fonction inferieur
               avaient accès ou non à certains droits pour m'assurer que les spécifications étaient respectées.`,
               images: [image36, image37, image38, image39, image40,image41, image42],
               competences: [
                   {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 3 | Faire des essais et évaluer leurs résultats en regard des spécifications'] },
                           { level: 'Niveau 2', acs: ['AC 1 | Élaborer et implémenter les spécifications fonctionnelles et non fonctionnelles à partir des exigences'] },
                       ]
                   },
                   {
                       name: 'Compétence 4',
                       levels: [
                           { level: 'Niveau 2', acs: ['AC 2 | Assurer la confidentialité des données (intégrité et sécurité)'] },
                       ]
                   },
               ]
           },
           {
               title: `Étape 14 : Implémentation de la fonctionnalité d'ajout de pièces jointes aux demandes`,
               text: `Il m’a été demandé d’ajouter des fichiers aux demandes, ce qui a nécessité une réflexion approfondie sur la gestion, 
               le stockage et la récupération de ces fichiers. J’ai élaboré la création d’un dossier "uploads" au lancement de l’application pour 
               y stocker tous les fichiers uploadés dans les demandes. Les données des fichiers sont cryptées et sécurisées dans l’application. Après avoir stocké les fichiers, 
               j’ai modifié le MCD en ajoutant une table "fichier" pour enregistrer le nom et le chemin des fichiers uploadés. Ensuite, j’ai utilisé des requêtes de l’API 
               pour récupérer et afficher les fichiers dans la vue de la demande, permettant également leur téléchargement. J’ai testé la fonctionnalité pour m’assurer que 
               les fichiers étaient correctement téléchargeables et affichés dans les demandes modifiées.`,
               images: [image43, image44,image45,image46],
               competences: [
                   {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 3 | Faire des essais et évaluer leurs résultats en regard des spécifications'] },
                           { level: 'Niveau 2', acs: ['AC 1 | Élaborer et implémenter les spécifications fonctionnelles et non fonctionnelles à partir des exigences',
                                   'AC 3 | Adopter de bonnes pratiques de conception et de programmation'] },
                       ]
                   },
                   {
                       name: 'Compétence 4',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 1 | Mettre à jour et interroger une base de données relationnelle (en requêtes directes ou à travers une application)'] },
                           { level: 'Niveau 2', acs: ['AC 1 | Optimiser les modèles de données de l’entreprise',
                                   'AC 4 | Manipuler des données hétérogènes'] },
                       ]
                   },
               ]
           },
           {
               title: `Étape 15 : Résolution des problèmes liés au stockage des fichiers uploadés`,
               text: `Après avoir testé l’application, j’ai identifié une erreur de duplication des fichiers où plusieurs demandes avec le même nom 
               de fichier causaient un bug, empêchant le fichier d’être correctement placé dans le dossier "uploads". Pour résoudre ce problème, j'ai 
               repensé la manière de stocker les fichiers en créant un sous-dossier dans "uploads" avec l'ID de la demande correspondante comme nom. Ainsi, 
               même si deux demandes différentes partagent le même nom de fichier, cela ne pose plus de problème. Cette solution a permis d'optimiser les modèles 
               de données en évitant les conflits de noms de fichiers et en assurant la bonne manipulation des données hétérogènes.`,
               images: [image51],
               competences: [
                   {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 2', acs: ['AC 1 | Élaborer et implémenter les spécifications fonctionnelles et non fonctionnelles à partir des exigences',
                                   'AC 4 | Vérifier et valider la qualité de l’application par les tests'] },
                       ]
                   },
               ]
           },
           {
            title: `Étape 16 : Implémentation de la fonctionnalité du motif lors de l'arbitrage`,
            text: `Lors de l’arbitrage des demandes, j’ai été chargé d’ajouter la fonctionnalité permettant d'ajouter un motif de refus ou de validation, 
            en suivant une hiérarchie avec des motifs spécifiques pour les responsables, les DGA, les DGS, etc. J'ai élaboré cette fonctionnalité en modifiant 
            le modèle conceptuel de données (MCD) de l’application pour intégrer ces nouveaux champs de motif. Ainsi, j’ai pu élaborer et implémenter les 
            spécifications fonctionnelles et non fonctionnelles à partir des exigences définies, tout en optimisant les modèles de données de l’entreprise pour 
            répondre aux besoins spécifiques de l’arbitrage des demandes`,
            images: [image47, image48, image49, image50],
            competences: [
                {
                    name: 'Compétence 1',
                    levels: [
                        { level: 'Niveau 2', acs: ['AC 1 | Élaborer et implémenter les spécifications fonctionnelles et non fonctionnelles à partir des exigences'] },
                    ]
                },
                {
                    name: 'Compétence 4',
                    levels: [
                        { level: 'Niveau 2', acs: ['AC 1 | Optimiser les modèles de données de l’entreprise'] },
                    ]
                }
            ]
        },
        ]);

        let slideshowInstance = null;
        let progress = ref(0);
        const fullscreenImage = ref(null);
        const currentImageIndex = ref(0);
        const modalImages = ref([]);

        onMounted(() => {
            slideshowInstance = new Slideshow(document.querySelector('.slideshow'));
        });

    class Slideshow {
        constructor(el) {
            this.DOM = { el: el };

            this.config = {
                slideshow: {
                    delay: 3000,
                    pagination: {
                        duration: 3,
                    },
                },
            };

            this.init();
        }
        init() {
            var self = this;
            this.DOM.el.addEventListener('touchstart', this.touchStartHandler.bind(this), { passive: true });
            this.DOM.el.addEventListener('touchend', this.touchEndHandler.bind(this), { passive: true });


            this.DOM.slideTitle = this.DOM.el.querySelectorAll('.slide-title');
            this.DOM.slideTitle.forEach((slideTitle) => {
                charming(slideTitle);
            });

            this.slideshow = new Swiper(this.DOM.el, {
                loop: true,
                autoplay: {
                    delay: this.config.slideshow.delay,
                    disableOnInteraction: false,
                },
                speed: 500,
                preloadImages: true,
                updateOnImagesReady: true,
                pagination: {
                    el: '.slideshow-pagination',
                    clickable: true,
                    bulletClass: 'slideshow-pagination-item',
                    bulletActiveClass: 'active',
                    clickableClass: 'slideshow-pagination-clickable',
                    modifierClass: 'slideshow-pagination-',
                    renderBullet: function (index, className) {
                        var slideIndex = index,
                            number = index <= 8 ? '0' + (slideIndex + 1) : slideIndex + 1;

                        var paginationItem = '<span class="slideshow-pagination-item">';
                        paginationItem += '<span class="pagination-number">' + number + '</span>';
                        paginationItem = index <= 8 ? paginationItem + '<span class="pagination-separator"><span class="pagination-separator-loader"></span></span>' : paginationItem;
                        paginationItem += '</span>';

                        return paginationItem;
                    },
                },
                navigation: {
                    nextEl: '.slideshow-navigation-button.next',
                    prevEl: '.slideshow-navigation-button.prev',
                },
                scrollbar: {
                    el: '.swiper-scrollbar',
                },
                on: {
                    init: function () {
                        self.animate('next');
                    },
                },
            });

            this.initEvents();
        }
        touchStartHandler(event) {
            this.touchStartX = event.touches[0].clientX;
        }
        touchEndHandler(event) {
            const touchEndX = event.changedTouches[0].clientX;
            const deltaX = touchEndX - this.touchStartX;

            // Mettez à jour la barre de progression uniquement si le glissement est significatif
            if (Math.abs(deltaX) > 50) {
                if (deltaX > 0) {
                    // Glissement vers la droite
                    this.prevSlide();
                } else {
                    // Glissement vers la gauche
                    this.nextSlide();
                }
                this.updateProgress();
            }
        }
        initEvents() {
            this.slideshow.on('paginationUpdate', (swiper, paginationEl) => this.animatePagination(swiper, paginationEl));
            this.slideshow.on('slideNextTransitionStart', () => this.animate('next'));
            this.slideshow.on('slidePrevTransitionStart', () => this.animate('prev'));
        }
        animate(direction = 'next') {
        this.DOM.activeSlide = this.DOM.el.querySelector('.swiper-slide-active');
        this.DOM.activeSlideTitle = this.DOM.activeSlide.querySelector('.slide-title');
        this.DOM.activeSlideText = this.DOM.activeSlide.querySelector('.slide-text');
        this.DOM.activeSlideTitleLetters = this.DOM.activeSlideTitle.querySelectorAll('span');
            
        this.DOM.activeSlideTitleLetters = direction === 'next' ? this.DOM.activeSlideTitleLetters : Array.from(this.DOM.activeSlideTitleLetters).reverse();
            
        this.DOM.oldSlide = direction === 'next' ? this.DOM.el.querySelector('.swiper-slide-prev') : this.DOM.el.querySelector('.swiper-slide-next');
        if (this.DOM.oldSlide) {
            this.DOM.oldSlideTitle = this.DOM.oldSlide.querySelector('.slide-title');
            this.DOM.oldSlideText = this.DOM.oldSlide.querySelector('.slide-text');
            this.DOM.oldSlideTitleLetters = this.DOM.oldSlideTitle.querySelectorAll('span');
            this.DOM.oldSlideTitleLetters.forEach((letter, pos) => {
                TweenMax.to(letter, .3, {
                    ease: Quart.easeIn,
                    delay: (this.DOM.oldSlideTitleLetters.length - pos - 1) * .04,
                    y: '0%',
                    opacity: 1
                });
            });
            TweenMax.to(this.DOM.oldSlideText, .3, {
                ease: Quart.easeIn,
                y: '0%',
                opacity: 1
            });
        }
    
        this.DOM.activeSlideTitleLetters.forEach((letter, pos) => {
            TweenMax.to(letter, .6, {
                ease: Back.easeOut,
                delay: pos * .05,
                startAt: { y: '50%', opacity: 0 },
                y: '0%',
                opacity: 1
            });
        });
        TweenMax.to(this.DOM.activeSlideText, .6, {
            ease: Back.easeOut,
            startAt: { y: '50%', opacity: 0 },
            y: '0%',
            opacity: 1
        });
    }
        animatePagination(swiper, paginationEl) {
            this.DOM.paginationItemsLoader = paginationEl.querySelectorAll('.pagination-separator-loader');
            this.DOM.activePaginationItem = paginationEl.querySelector('.slideshow-pagination-item.active');
            this.DOM.activePaginationItemLoader = this.DOM.activePaginationItem.querySelector('.pagination-separator-loader');

            TweenMax.set(this.DOM.paginationItemsLoader, { scaleX: 0 });
            TweenMax.to(this.DOM.activePaginationItemLoader, this.config.slideshow.pagination.duration, {
                startAt: { scaleX: 0 },
                scaleX: 1,
            });
        }
    }

    return {
      slides,
      progress,
      fullscreenImage,
      modalImages,
      currentImageIndex,
      activeSlideIndex: 0, // Indice de la diapositive actuellement active
    goToSlide(index) {
      this.activeSlideIndex = index; // Met à jour l'indice de la diapositive active
    },
      prevSlide() {
        slideshowInstance.slideshow.slidePrev();
        this.updateProgress();
      },
      nextSlide() {
        slideshowInstance.slideshow.slideNext();
        this.updateProgress();
      },
      updateProgress() {
        progress.value = ((slideshowInstance.slideshow.realIndex + 1) / slides.value.length) * 100;
      },
      openImage(images, index) {
        modalImages.value = images;
        currentImageIndex.value = index;
        fullscreenImage.value = images[index];
      },
      closeImage() {
        fullscreenImage.value = null;
      },
      prevModalImage() {
        if (currentImageIndex.value > 0) {
          currentImageIndex.value--;
          fullscreenImage.value = modalImages.value[currentImageIndex.value];
        }
      },
      nextModalImage() {
        if (currentImageIndex.value < modalImages.value.length - 1) {
          currentImageIndex.value++;
          fullscreenImage.value = modalImages.value[currentImageIndex.value];
        }
      },
    };
  },
};
</script>

<style scoped>

.image-indicators {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}

.indicator {
  width: 10px;
  height: 10px;
  background-color: #ccc; /* Couleur des points inactifs */
  border-radius: 50%;
  margin: 0 5px; /* Espacement entre les points */
  cursor: pointer; /* Curseur de pointeur */
}

.indicator.active {
  background-color: #EB5E28; /* Couleur du point actif */
}
.image-container {
  position: relative;
  overflow: hidden;
  cursor: pointer; 
}

.slide-image {
  max-width: 100%;
  max-height: 90%;
  transition: transform 0.3s ease;
}

.image-container:hover .slide-image {
  transform: scale(1.05); 
}
.fullscreen-image-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  z-index: 2;
}
.fullscreen-image-modal img {
  max-width: 80%;
  max-height: 60%;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
}
.close-button {
  position: absolute;
  top: 15%;
  right: 15%;
  background: none;
  border: none;
  color: white;
  font-size: 24px;
  cursor: pointer;
}
.modal-nav-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: none;
  border: none;
  color: white;
  font-size: 24px;
  cursor: pointer;
}
.modal-nav-button.left {
  left: 20px;
}
.modal-nav-button.right {
  right: 20px;
}
/* Nouveau style pour les groupes d'AC */
.ac-group {
    display: flex; /* Afficher les AC en ligne */
    flex-wrap: wrap; /* Permettre le retour à la ligne si nécessaire */
}

/* Ligne horizontale personnalisée */
.custom-line {
    width: 60px; /* Ajustez la largeur de la ligne */
    height: 3px; /* Ajustez l'épaisseur de la ligne */
    background-color: #252422; /* Ajustez la couleur de la ligne */
    margin: 20px auto; /* Centre la ligne horizontalement et ajoute de l'espace autour */
}

/* Titre Apprentissage Critique */
.learning-title {
    font-size: 22px;
    text-align: center;
    margin-top: 40px;
    color: #252422;
}

/* Conteneur de la section Apprentissage Critique */
.learning-container {
    display: flex;
    margin-top: 20px;
}

/* Bloc pour chaque compétence */
.competence-block {
    margin-left: 30px;
    width: 100%; /* Ajustez la largeur des blocs si nécessaire */
}

/* Style pour les niveaux */
.level {
    margin-bottom: 2%;
}

/* Titre pour les compétences */
.competence-block h3 {
    font-size: 15px;
    margin-bottom: 10px;
    color: #252422;
}

/* Titre pour les niveaux */
.level h4 {
    font-size: 14px;
    margin-bottom: 5px;
    color: #EB5E28;
}

p {
    font-size: 12px;
}

.slide-subtitle {
    font-size: 16px;
    color: #252422;
    margin-top: 10px;
}
.slide-subtitle::after {
    content: '';
    display: block;
    width: 60px;
    height: 3px;
    background-color: #252422;
    margin-top: 8px;
}
.sous-titre {
    font-size: 20px;
    text-align: center;
}

.slideshow-progress {
    width: 100%;
    height: 5px;
    background-color: #FFFCF2;
    position: relative;
}

.progress-bar {
    height: 100%;
    background-color: #EB5E28; /* Mettez la couleur verte ici */
    width: 0%;
    transition: width 0.3s ease;
}
.fa-chevron-right {
    margin-left: 4px;
}

.fa-chevron-left {
    margin-right: 4px;
}

.container-top {
    min-height: 100vh;
    padding-top: 125px;
    background: #FFFCF2;
}

/* Style pour chaque cercle (AC) */
.circle {
    display: flex;
    width: 100%;
    height: 100%;
    background-color: #ccc5b9;
    padding: 5px;
    border-radius: 8px;
    margin-bottom: 10px; /* Espace entre les cercles */
    margin-right: 10px; /* Espace entre les cercles */
}

h1.main-title {
    color: #252422;
    text-align: center;
    margin-bottom: 2%;
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

.swiper-container {
    width: 100%;
    max-width: 100%;
    min-height: 75vh;
    position: relative;
    overflow: hidden;
}

.swiper-wrapper {
    display: flex;
    align-items: center;
}

.swiper-slide {
    display: flex;
    align-items: center;
    justify-content: center;
}

.slide-card {
    background-color: #FFFCF2;
    padding-right: 90px;
    padding-left: 90px;
    width: 100%;
    max-width: 100%;
    height: 100%;
    display: flex;
}

.text-content {
    width: 50%;
    padding-bottom: 55px;
    padding-left: 3%;
    padding-top: 3%;
    text-align: left;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
}

.image-content {
    width: 50%;
    align-content: center;
    text-align: center;
}

.slide-title {
    font-size: 21px;
    margin-bottom: 2%;
    position: relative; /* Assurez-vous que l'élément parent est positionné */
}
.slide-title::after {
    content: '';
    display: block;
    width: 60px; /* Ajustez la largeur de la barre selon vos besoins */
    height: 3px; /* Ajustez la hauteur de la barre selon vos besoins */
    background-color: #252422; /* Ajustez la couleur de la barre selon vos besoins */
    margin-top: 8px; /* Espace entre le titre et la barre */
}

.slide-text {
    font-size: 16px;
    margin-left: 10px;
    margin-bottom: 2%;
    width: 100%;
    color: #252422;
}

.slide-image {
    max-width: 60%;
    height: auto;
    border-radius: 5%;

}

.slideshow-pagination {
    position: absolute;
    bottom: 20px;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    align-items: center;
}

.slideshow-pagination-item {
    margin: 0 5px;
    cursor: pointer;
}

  .slideshow-navigation {
    position: absolute;
    top: 50%;
    width: 100%;
    display: flex;
    justify-content: space-between;
    transform: translateY(-50%);
    padding: 0 20px;
    box-sizing: border-box;
    z-index: 1;
  }

.slideshow-navigation-button {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    width: 40px;
    height: 40px;
    line-height: 40px;
    text-align: center;
    font-size: 24px;
    font-weight: bold;
    color: #252422;
    border-radius: 50%;
    cursor: pointer;
    z-index: 1;
    transition: background-color 0.3s;
}

/* Styles pour la flèche de gauche */
.slideshow-navigation-button.prev {
    left: 3%;
}

/* Styles pour la flèche de droite */
.slideshow-navigation-button.next {
    right: 3%;
}

.slideshow-navigation-button-L i {
    transition: transform 0.5s ease-in-out;
}
.slideshow-navigation-button-L:hover i {
    transform: translateX(-10px); /* Décale la flèche vers le bas lorsqu'elle est survolée */
}

.slideshow-navigation-button-R i {
    transition: transform 0.5s ease-in-out;
}
.slideshow-navigation-button-R:hover i {
    transform: translateX(10px); /* Décale la flèche vers le bas lorsqu'elle est survolée */
}

  </style>
