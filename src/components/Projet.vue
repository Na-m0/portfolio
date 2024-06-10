<template>
    <section class="container-top">
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
                            <div v-for="competence in slide.competences" :key="competence.name" class="competence-block">
                                <h3>{{ competence.name }}</h3>
                                <div v-for="level in competence.levels" :key="level.level" class="level">
                                    <h4>{{ level.level }}</h4>
                                    <!-- Ajoutez cette condition pour grouper les AC du même niveau -->
                                    <div class="ac-group" v-if="level.acs.length > 1">
                                        <div class="circle" v-for="ac in level.acs" :key="ac">{{ ac }}</div>
                                    </div>
                                    <!-- Utilisez cette div si vous avez un seul AC par niveau -->
                                    <div class="circle" v-else>{{ level.acs[0] }}</div>
                                </div>
                            </div>
                        </div>
                        </div>
                        <div class="image-content">
                            <img :src="slide.image" alt="Slide image" class="slide-image"/>
                        </div>
                    </div>
                </div>
            </div>

            <div class="slideshow-pagination"></div>
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
    </section>
</template>

<script>
import { onMounted, ref } from 'vue';
import Swiper from 'swiper';
import 'swiper/swiper-bundle.css';
import charming from 'charming';
import { TweenMax, Back, Expo, Quart } from 'gsap';
import image1 from '../assets/Mairie_de_Montbéliard.jpg';
import image2 from '../assets/Mairie_de_Montbéliard.jpg';
import image3 from '../assets/Mairie_de_Montbéliard.jpg';
import image4 from '../assets/Mairie_de_Montbéliard.jpg';
import image5 from '../assets/Mairie_de_Montbéliard.jpg';
import image6 from '../assets/Mairie_de_Montbéliard.jpg';
import image7 from '../assets/Mairie_de_Montbéliard.jpg';
import image8 from '../assets/Mairie_de_Montbéliard.jpg';
import image9 from '../assets/Mairie_de_Montbéliard.jpg';
import image10 from '../assets/Mairie_de_Montbéliard.jpg';
import image11 from '../assets/Mairie_de_Montbéliard.jpg';
import image12 from '../assets/Mairie_de_Montbéliard.jpg';
import image13 from '../assets/Mairie_de_Montbéliard.jpg';
import image14 from '../assets/Mairie_de_Montbéliard.jpg';
import image15 from '../assets/Mairie_de_Montbéliard.jpg';
import image16 from '../assets/Mairie_de_Montbéliard.jpg';

export default {
    setup() {
    const slides = ref([
    {
                title: 'Étape 1',
                text: `Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec id tellus in diam eleifend dignissim nec et dolor. 
                Duis tincidunt, diam eget eleifend vestibulum, felis mauris consequat velit, id ullamcorper ligula nisi at ante. Duis vitae 
                blandit quam. Phasellus nec nulla libero. Phasellus aliquam ante urna, ac auctor est suscipit vel. Suspendisse sagittis augue
                eget semper malesuada. Phasellus mollis sed dolor sed interdum. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec
                id tellus in diam eleifend dignissim nec et dolor. Duis tincidunt, diam eget eleifend vestibulum, felis mauris consequat velit, 
                id ullamcorper ligula nisi at ante. Duis vitae blandit quam. Phasellus nec nulla libero. Phasellus aliquam ante urna, ac auctor 
                est suscipit vel. Suspendisse sagittis augue eget semper malesuada. Phasellus mollis sed dolor sed interdum.`,
                image: image1,
                competences: [
                    {
                        name: 'Compétence 1',
                        levels: [
                            { level: 'Niveau 1', acs: ['AC 1', 'AC 2', 'AC 3', 'AC 4'] },
                            { level: 'Niveau 2', acs: ['AC 1', 'AC 2', 'AC 3', 'AC 4'] }
                        ]
                    },
                    {
                        name: 'Compétence 4',
                        levels: [
                            { level: 'Niveau 1', acs: ['AC 1', 'AC 2', 'AC 3'] },
                            { level: 'Niveau 2', acs: ['AC 1', 'AC 2', 'AC 3', 'AC 4'] }
                        ]
                    }
                ]
            },
            {
                title: 'Étape 2',
                text: `Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec id tellus in diam eleifend dignissim nec et dolor. 
                Duis tincidunt, diam eget eleifend vestibulum, felis mauris consequat velit, id ullamcorper ligula nisi at ante. Duis vitae 
                blandit quam. Phasellus nec nulla libero. Phasellus aliquam ante urna, ac auctor est suscipit vel. Suspendisse sagittis augue
                eget semper malesuada. Phasellus mollis sed dolor sed interdum.`,
                image: image2,
                competences: [
                    {
                        name: 'Compétence 4',
                        levels: [
                            { level: 'Niveau 1', acs: ['AC 1', 'AC 3'] },
                            { level: 'Niveau 2', acs: ['AC 2', 'AC 4'] }
                        ]
                    }
                ]
            },
            {
                title: 'Étape 3',
                text: `Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec id tellus in diam eleifend dignissim nec et dolor. 
                Duis tincidunt, diam eget eleifend vestibulum, felis mauris consequat velit, id ullamcorper ligula nisi at ante. Duis vitae 
                blandit quam. Phasellus nec nulla libero.`,
                image: image3,
                competences: [
                    {
                        name: 'Compétence 4',
                        levels: [
                            { level: 'Niveau 1', acs: ['AC 1', 'AC 2'] },
                            { level: 'Niveau 2', acs: ['AC 1', 'AC 4'] }
                        ]
                    }
                ]
            }
        ]);

        let slideshowInstance = null;
        let progress = ref(0);

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
            this.DOM.el.addEventListener('touchstart', this.touchStartHandler.bind(this));
            this.DOM.el.addEventListener('touchend', this.touchEndHandler.bind(this));

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
            }
        };
    }
};
</script>

<style scoped>
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
    justify-content: space-around;
    margin-top: 20px;
}

/* Bloc pour chaque compétence */
.competence-block {
    width: 45%; /* Ajustez la largeur des blocs si nécessaire */
}

/* Style pour les niveaux */
.level {
    margin-bottom: 20px;
}

/* Titre pour les compétences */
.competence-block h3 {
    font-size: 18px;
    margin-bottom: 10px;
    color: #252422;
}

/* Titre pour les niveaux */
.level h4 {
    font-size: 16px;
    margin-bottom: 5px;
    color: #EB5E28;
}

/* Texte des AC */
.level p {
    font-size: 14px;
    color: #252422;
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
    font-size: 17px;
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
    height: 85vh;
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
    height: 101%;
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
    padding-top: 55px;
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
    font-size: 24px;
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
    max-width: 80%;
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
