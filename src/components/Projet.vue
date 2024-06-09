<template>
    <section class="container-top">
        <h1 class="main-title">PROJET</h1>
        <h1 class="overlay-title">PROJET</h1>
        <div class="swiper-container slideshow">
            <div class="swiper-wrapper">
                <div class="swiper-slide slide" v-for="(slide, index) in slides" :key="index">
                    <div class="slide-card">
                        <div class="text-content">
                            <h2 class="slide-title">{{ slide.title }}</h2>
                            <p class="slide-text">{{ slide.text }}</p>
                        </div>
                        <div class="image-content">
                            <img :src="slide.image" alt="Slide image" class="slide-image"/>
                        </div>
                    </div>
                </div>
            </div>

            <div class="slideshow-pagination"></div>
            <div class="slideshow-navigation">
                <div class="slideshow-navigation-button prev">❮</div>
                <div class="slideshow-navigation-button next">❯</div>
            </div>
        </div>
    </section>
</template>

<script>
import { onMounted, ref } from 'vue';
import Swiper from 'swiper';
import 'swiper/swiper-bundle.css';
import charming from 'charming';
import { TweenMax, Back, Expo, Quart } from 'gsap';

export default {
    setup() {
        const slides = ref([
            {
                title: 'Étape 1',
                text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec id tellus in diam eleifend dignissim nec et dolor. Duis tincidunt, diam eget eleifend vestibulum, felis mauris consequat velit, id ullamcorper ligula nisi at ante. Duis vitae blandit quam. Phasellus nec nulla libero. Phasellus aliquam ante urna, ac auctor est suscipit vel. Suspendisse sagittis augue eget semper malesuada. Phasellus mollis sed dolor sed interdum.',
                image: '/src/assets/gear5.webp',
            },
            {
                title: 'Meet ocean',
                text: 'Experience the beauty and mystery of the ocean.',
                image: 'path/to/image2.jpg',
            },
            {
                title: 'Around the world',
                text: 'Travel around the world and explore new cultures.',
                image: 'path/to/image3.jpg',
            },
            // Ajoutez d'autres slides ici
        ]);

        onMounted(() => {
            const slideshow = new Slideshow(document.querySelector('.slideshow'));
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
        };
    },
};
</script>

<style scoped>
.container-top {
    height: 100vh;
    padding-top: 125px;
    background: #FFFCF2;
}

h1.main-title {
    color: #252422;
    text-align: center;
    margin-bottom: 45px;
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
    height: 76vh;
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
    padding: 90px;
    width: 100%;
    max-width: 100%;
    height: 100%;
    display: flex;
}

.text-content {
    width: 50%;
    padding: 55px;
    text-align: left;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
}

.image-content {
    width: 50%;
    align-content: center;
    text-align: right;
}

.slide-title {
    font-size: 24px;
    margin-bottom: 10px;
}

.slide-text {
    font-size: 16px;
    color: #252422;
}

.slide-image {
    max-width: 100%;
    height: auto;
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
    background: rgba(0, 0, 0, 0.5);
    color: #fff;
    border-radius: 50%;
    cursor: pointer;
    z-index: 10;
    transition: background-color 0.3s;
}

/* Styles pour la flèche de gauche */
.slideshow-navigation-button.prev {
    left: 20px;
}

/* Styles pour la flèche de droite */
.slideshow-navigation-button.next {
    right: 20px;
}

/* Au survol, assombrissez légèrement la couleur de fond */
.slideshow-navigation-button:hover {
    background-color: rgba(0, 0, 0, 0.7);
}
  </style>
