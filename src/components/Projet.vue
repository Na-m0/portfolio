<template>
    <div class="container-top">
      <h1 class="main-title">PROJET</h1>
      <h1 class="overlay-title">PROJET</h1>
      <p class="sous-titre">Voici donc tout l’avancer du projet qui m’a permis de valider les compétences présentées</p>
      <div class="swiper-container slideshow">
        <div class="swiper-wrapper">
          <div class="swiper-slide slide" v-for="(slide, index) in slides" :key="index">
            <div class="slide-card">
              <div class="text-content">
                <h2 class="slide-title">{{ slide.title }}</h2>
                <p class="slide-text">{{ slide.text }}</p>
                <h3 class="slide-subtitle">Apprentissage critique validé</h3>
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
    setup() {
    const slides = ref([
           {
               title: `Étape 1 : Analyse du cahier des charges`,
               text: `Grâce au cahier des charges qu' il y a eu, j’ai pu réfléchir à des schéma afin d’avoir une
               visualisation de comment gérer l’application et de voir tout ce dont il y a besoin.`,
               images: [image1,image2,image3,image4,image5], // Liste des images pour cette slide
               competences: [
                   {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 2'] },
                       ]
                   },
               ]
           },
           {
               title:`Étape 2 : Réflexion et conception initiale du modèle de données de l'application`,
               text: ` J’ai pu réfléchir à un premier MCD à partir des données qui était demandé dans le cahier des charge,
               tel que l’agent, la hiérarchie des fonctions, les demandes, …etc`,
               images: [image6,image7],
               competences: [
                   {
                       name: 'Compétence 4',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 3'] },
                       ]
                   },
               ]
           },
           {
               title: 'Étape 3 : Création de la base de données (BDD) pour le projet',
               text: `J’ai, grâce au MCD, créé la BDD du projet afin de visualiser des données et de les manipuler.
               Notamment grâce au requête (PUT, GET, POST et DELETE) de l'API que j’ai développé.`,
               images: [image11, image10, image12],
               competences: [
                   {
                       name: 'Compétence 4',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 1', 'AC 3'] },
                       ]
                   },
               ]
           },
           {
               title: 'Étape 4 : Utilisation de Figma pour créer la maquette du site',
               text: `Afin d’y voir clair sur l’application et de ne pas avancer au hasard, j’ai décidé de créer des
               maquettes des pages principales pour les utilisateurs. Cela m’a aidé à coder les pages plus facilement. \n
               Cela va aussi permettre d’arranger les différents modules de l’app de la manière la plus ergonomique possible.`,
               images: [image14,image13],
               competences: [
                   {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 2'] },
                           { level: 'Niveau 2', acs: ['AC 2'] },
                       ]
                   },
               ]
           },
           {
               title: `Étape 5 : Développement de l'interface utilisateur avec Vue.js`,
               text: `J’ai donc créé la vue du projet en mettant les différents modules MVC (Model, Vue, Controller)
               qui permettent une vision claire du code.\n
               J’ai pu élaborer une page de connexion avec des champs qui permettent de se connecter. \n
               Cela fait partie de l’interface utilisateur.`,
               images: [image15, image52, image53, image54, image55, image56],
               competences: [
                   {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 1', 'AC 4'] },
                           { level: 'Niveau 2', acs: ['AC 3'] },
                       ]
                   },
               ]
           },
           {
                title: `Étape 6 : Implémentation de la gestion des tokens et des utilisateurs`,
                text: `Afin de compléter la connexion, j’ai élaboré une fonction de gestion de tokens lors de l’identification.\n
                Tout cela en utilisant un “store” de l’application afin d’avoir la possibilité de réutilisation du code \n
                Comme il y a un token lors de l'identification, cela va permettre au utilisateur d'être géré et
                d’avoir certain droit d'utilisation.`,
                images: [image16, image17, image18],
                competences: [
                    {
                        name: 'Compétence 1',
                        levels: [
                            { level: 'Niveau 2', acs: ['AC 1', 'AC 3'] },
                        ]
                    },
                    {
                        name: 'Compétence 4',
                        levels: [
                            { level: 'Niveau 2', acs: ['AC 2'] },
                        ]
                    },
                ]
            },
           {
                title: `Étape 7 : Affichage des demandes du service lors de la connexion de l'utilisateur`,
                text: `J’ai créé des requêtes pour la page des demandes afin d’afficher les demandes du service
                auquel l’agent est relié. Ces requêtes vont permettre d’afficher toutes les demandes dans la vue de l’application.
                J’ai donc testé si la visualisation affichait correctement les bonnes demandes liées au services.`,
                images: [image57,image58, image59,image19],
                competences: [
                    {
                        name: 'Compétence 1',
                        levels: [
                            { level: 'Niveau 1', acs: ['AC 3'] },
                            { level: 'Niveau 2', acs: ['AC 1'] },
                        ]
                    },
                    {
                        name: 'Compétence 4',
                        levels: [
                            { level: 'Niveau 2', acs: ['AC 1'] },
                        ]
                    },
                ]
            },
           {
               title: `Étape 8 : Limitation des actions des différents agents`,
               text: `Les agents devaient avoir une fonction afin d’avoir une hiérarchie sur les arbitrages et la
               visualisation des données des demandes. j’ai donc modifier le MCD afin de régler les problèmes de hiérarchies.`,
               images: [image8],
               competences: [
                   {
                       name: 'Compétence 4',
                       levels: [
                           { level: 'Niveau 2', acs: ['AC 1','AC 2', 'AC 3'] },
                       ]
                   },
               ]
           },
           {
               title: `Étape 9 : Amélioration graphique de l'application`,
               text: `Afin de rendre comme le figma j'ai refait tout le design de l'application. Cela m'a pris beaucoup de temps mais cela étais tres important 
               pour l'experience utilisateur, il fallait que les personnes qui test l'application, puissent apprécier et surtout comprendre ce qu'il voyait`,
               images: [image20, image21],
               competences: [
                   {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 3', 'AC 4'] },
                           { level: 'Niveau 2', acs: ['AC 2'] },
                       ]
                   }
               ]
           },
           {
               title: `Étape 10 : Ajout de fonctionnalités à la page d'accueil`,
               text: `Afin d’améliorer l'expérience de l'utilisateur, j’ai décidé de rajouter des petites indications
               sur le ou les services qui lui sont reliés. J’ai donc ajouté des requêtes de l’API afin d’obtenir les
               données souhaitées, tel que le nombre de demandes, le budget total des demandes et les différents statuts
               des demandes. Toutes les requêtes interrogent la BDD pour obtenir les données souhaitées qui sont ensuite
               affichées dans la vue de l’utilisateur. Tout cela en vérifiant si les données récupérées sont bien les
               bonnes et qu’aucun bug n’intervient.`,
               images: [image22, image26, image23, image24, image25],
               competences: [
                   {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 3', 'AC 4'] },
                           { level: 'Niveau 2', acs: ['AC 1'] },
                       ]
                   },
                   {
                       name: 'Compétence 4',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 1'] },
                       ]
                   },
               ]
           },
           {
               title: `Étape 11 : Développement des pages d'ajout et de modification de demandes`,
               text: `Si il y a des demandes c’est qu’il doit être possible d’en ajouter et de les modifier.
               J’ai donc ajouté les pages d’ajout et de modification des demandes, et cela en prenant compte des
               informations écrites dans le cahier des charge a mettre lors de l’ajout et de la modification.
               Les données sont donc modifier, ajouter et visualiser grâce au requete de l’API, cela va donc permettre une
               gestion des demandes par les utilisateurs. Et toujours en vérifiant que les données sont bien ajoutées ou modifiées.`,
               images: [image31, image27, image28, image29, image30],
               competences: [
                   {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 3'] },
                           { level: 'Niveau 2', acs: ['AC 1'] },
                       ]
                   },
                   {
                       name: 'Compétence 4',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 1'] },
                       ]
                   },
               ]
           },
           {
            title: `Étape 12 : Implémentation de la connexion d'un Directeur Général Adjoint`,
            text: `Dans cette aplication il y aura une hierarchie des agents, il faut donc grace au fonction ajouter
            dans la table gérer qui aura certain droit dans la vue. J'ai donc implémenter des fonctions afin de
            différencier un agent commun d'un directeur. Le directeur aura acces a la liste des services qu'il gere et pourra donc
            voir, modifier ou supprimer les demandes de ses services.`,
            images: [image32, image33, image34, image35],
            competences: [
                {
                    name: 'Compétence 1',
                    levels: [
                        { level: 'Niveau 1', acs: ['AC 3', 'AC 4'] },
                        { level: 'Niveau 2', acs: ['AC 1', 'AC 2'] },
                    ]
                },
                {
                    name: 'Compétence 4',
                    levels: [
                        { level: 'Niveau 1', acs: ['AC 1','AC 2'] },
                        { level: 'Niveau 2', acs: ['AC 1','AC 2'] },
                    ]
                },
            ]
        },
           {
               title: `Étape 13 : Implémentation de la fonctionnalité d'arbitrage des demandes`,
               text: `Comme le but de l’application est de gérer des demandes selon différentes hiérarchies,
               j’ai donc élaboré le système d’arbitrage de la demande qui update le statut de la demande lors de
               la validation ou le refus de la demande. Et cela change le stade de validation lorsque le compte
               d’un responsable ou un directeur arbitre la demande. Les utilisateurs en dessous des directeurs ne
               pourront donc plus avoir accès au modification ou au suppression de la demande lorsque celle- ci sera
               arbitrée. Cela permet donc une sécurité de gestion de données selon la fonction des utilisateurs. J’ai aussi
               testé si les utilisateurs lambda en dessous des responsables avaient accès ou non à certaines fonctions.`,
               images: [image36, image37, image38, image39, image40,image41, image42],
               competences: [
                   {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 3'] },
                           { level: 'Niveau 2', acs: ['AC 1'] },
                       ]
                   },
                   {
                       name: 'Compétence 4',
                       levels: [
                           { level: 'Niveau 2', acs: ['AC 2'] },
                       ]
                   },
               ]
           },
           {
               title: `Étape 14 : Implémentation de la fonctionnalité d'ajout de pièces jointes aux demandes`,
               text: ` Il m’a été demandé l’ajout de fichier à la demande, j’ai donc réfléchi longuement à comment gérer
               ces fichiers, où les stocker et comment les récupérer. J’ai donc élaboré une création d’un dossier uploads
               lors du lancement de l’application ce qui permettra d’y stocker tous les fichiers uploadés dans la demande.
               Les données des fichiers sont donc cryptées et stockées dans l’application.  Après avoir stocké ces fichiers,
               il fallait les récupérer afin de les afficher et de les télécharger. J’ai donc eu l'idée de modifier le MCD et
               d’y ajouter une table fichier afin d’y stocker le nom du fichier et le chemin où il a été uploadé. Enfin,
               après avoir stocké le nom des fichiers et leurs chemins dans la table fichier, j’ai utilisé des requêtes
               de l’API afin de récupérer le fichier et de l’afficher dans la vue de la demande et d’avoir la possibilité
               de le télécharger. Tout cela en testant que les fichier sont bien téléchargeable et afficher a la demande modifié.`,
               images: [image43, image44,image45,image46],
               competences: [
                   {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 3'] },
                           { level: 'Niveau 2', acs: ['AC 1', 'AC 3'] },
                       ]
                   },
                   {
                       name: 'Compétence 4',
                       levels: [
                           { level: 'Niveau 1', acs: ['AC 1'] },
                           { level: 'Niveau 2', acs: ['AC 1', 'AC 4'] },
                       ]
                   },
               ]
           },
           {
               title: `Étape 15 : Résolution des problèmes liés au stockage des fichiers uploadés`,
               text: ` Après avoir tester l’application, il y avait une erreur de duplication, c'est-à-dire que lorsque
               l’on mettait le même nom de fichier cela produisait un bug et ça ne mettait pas le fichier dans le dossier
               upload. J’ai donc réfléchi à une autre manière de stocker ces fichiers en créer un autre dossier dans le
               fichier upload avec comme nom l’id de la demande choisie. Cela ne pose donc plus de problème lorsque deux
               demandes différentes possèdent le même nom de fichier.`,
               images: [image51],
               competences: [
                   {
                       name: 'Compétence 1',
                       levels: [
                           { level: 'Niveau 2', acs: ['AC 1', 'AC 4'] },
                       ]
                   },
               ]
           },
           {
            title: `Étape 15 : Implémentation de la fonctionnalité du motif lors de l'arbitrage`,
            text: ` Lors de l’arbitrage des demandes, on m’a demandé d’ajouter un motif si c' est un refus ou une
            validation. J’ai donc élaboré cette fonctionnalité qui s’effectue aussi de façon hiérarchique avec un
            motif de responsable, de DGA, de DGS,... . Il a donc fallu une modification du MCD de l’application.`,
            images: [image47, image48, image49, image50],
            competences: [
                {
                    name: 'Compétence 1',
                    levels: [
                        { level: 'Niveau 2', acs: ['AC 1'] },
                    ]
                },
                {
                    name: 'Compétence 4',
                    levels: [
                        { level: 'Niveau 2', acs: ['AC 1'] },
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
            this.DOM.activeSlide = this.DOM.el.querySelector('.swiper-slide-active'),
                this.DOM.activeSlideTitle = this.DOM.activeSlide.querySelector('.slide-title'),
                this.DOM.activeSlideText = this.DOM.activeSlide.querySelector('.slide-text'),
                this.DOM.activeSlideTitleLetters = this.DOM.activeSlideTitle.querySelectorAll('span');

            this.DOM.activeSlideTitleLetters = direction === 'next' ? this.DOM.activeSlideTitleLetters : [].slice.call(this.DOM.activeSlideTitleLetters).reverse();

            this.DOM.oldSlide = direction === 'next' ? this.DOM.el.querySelector('.swiper-slide-prev') : this.DOM.el.querySelector('.swiper-slide-next');
            if (this.DOM.oldSlide) {
                this.DOM.oldSlideTitle = this.DOM.oldSlide.querySelector('.slide-title'),
                    this.DOM.oldSlideText = this.DOM.oldSlide.querySelector('.slide-text'),
                    this.DOM.oldSlideTitleLetters = this.DOM.oldSlideTitle.querySelectorAll('span');
                this.DOM.oldSlideTitleLetters.forEach((letter, pos) => {
                    TweenMax.to(letter, .3, {
                        ease: Quart.easeIn,
                        delay: (this.DOM.oldSlideTitleLetters.length - pos - 1) * .04,
                        y: '50%',
                        opacity: 0
                    });
                });
                TweenMax.to(this.DOM.oldSlideText, .3, {
                    ease: Quart.easeIn,
                    y: '50%',
                    opacity: 0
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
    margin-left: 5%;
    margin-top: 20px;
}

/* Bloc pour chaque compétence */
.competence-block {
    width: 45%; /* Ajustez la largeur des blocs si nécessaire */
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
    align-items: center;
    justify-content: center;
    width: 58px;
    height: 27px;
    background-color: #ccc5b9;
    border-radius: 20px;
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
