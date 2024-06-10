<template>
<body>
  <footer class="footer">
    
    <ul class="social-icon">
      <li class="social-icon__item"><a class="social-icon__link" href="https://github.com/Na-m0">
          <i class="fab fa-github"></i>
        </a></li>
      <li class="social-icon__item"><a class="social-icon__link" href="https://x.com/NGirods">
          <i class="fab fa-twitter"></i>
        </a></li>
      <li class="social-icon__item"><a class="social-icon__link" href="https://www.linkedin.com/in/noam-joly-girods-3a27b62a4/">
          <i class="fab fa-linkedin"></i>
        </a></li>
      <li class="social-icon__item"><a class="social-icon__link" href="https://www.instagram.com/nam0_jg/?next=%2F">
          <i class="fab fa-instagram"></i>
        </a></li>
    </ul>
    <ul class="menu">
      <li class="menu__item"><a class="menu__link" href="#accueil" @click.prevent="scrollToSection('accueil')">Accueil</a></li>
      <li class="menu__item"><a class="menu__link" href="#contexte" @click.prevent="scrollToSection('contexte')">Contexte</a></li>
        <li class="menu__item"><a class="menu__link" href="#competence" @click.prevent="scrollToSection('competence')">Compétences</a></li>
        <li class="menu__item"><a class="menu__link" href="#projet" @click.prevent="scrollToSection('projet')">Projet</a></li>
    </ul>
    <p>&copy;2024 Noam JOLY-GIRODS | All Rights Reserved</p>
  </footer>
</body>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue';

export default {
    name: 'NavBar',
    setup() {
        const isScrolled = ref(false);

        const handleScroll = () => {
            isScrolled.value = window.scrollY > 50;
        };

        onMounted(() => {
            window.addEventListener('scroll', handleScroll);
        });

        onUnmounted(() => {
            window.removeEventListener('scroll', handleScroll);
        });

        const scrollToSection = (sectionId) => {
            const section = document.getElementById(sectionId);
            if (section) {
                section.scrollIntoView({ behavior: 'smooth' });
            }
        };

        return {
            scrollToSection,
        };
    }
};
</script>

<style scoped>

body {
  display: flex;
  background: #252422;
  justify-content: flex-end;
  align-items: flex-end;
  min-height: 80vh;
}

.footer {
  position: relative;
  width: 100%;
  min-height: 100px;
  padding: 20px 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.social-icon,
.menu {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 10px 0;
  flex-wrap: wrap;
}

.social-icon__item,
.menu__item {
  list-style: none;
}

.social-icon__link {
  font-size: 2rem;
  color: #fff;
  margin: 0 10px;
  display: inline-block;
  transition: 0.5s;
}
.social-icon__link:hover {
  transform: translateY(-10px);
}

.menu__link {
  font-size: 1.2rem;
  color: #fff;
  margin: 0 10px;
  display: inline-block;
  transition: 0.5s;
  text-decoration: none;
  opacity: 0.75;
  font-weight: 300;
}

.menu__link:hover {
  opacity: 1;
}

.footer p {
  color: #fff;
  margin: 15px 0 10px 0;
  font-size: 1rem;
  font-weight: 300;
}

.wave {
  position: absolute;
  top: -100px;
  left: 0;
  width: 100%;
  height: 100px;
  background: url("https://i.ibb.co/wQZVxxk/wave.png");
  background-size: 1000px 100px;
}

.wave#wave1 {
  z-index: 1000;
  opacity: 1;
  bottom: 0;
  animation: animateWaves 4s linear infinite;
}

.wave#wave2 {
  z-index: 999;
  opacity: 0.5;
  bottom: 10px;
  animation: animate 4s linear infinite !important;
}

.wave#wave3 {
  z-index: 1000;
  opacity: 0.2;
  bottom: 15px;
  animation: animateWaves 3s linear infinite;
}

.wave#wave4 {
  z-index: 999;
  opacity: 0.7;
  bottom: 20px;
  animation: animate 3s linear infinite;
}

@keyframes animateWaves {
  0% {
    background-position-x: 1000px;
  }
  100% {
    background-positon-x: 0px;
  }
}

@keyframes animate {
  0% {
    background-position-x: -1000px;
  }
  100% {
    background-positon-x: 0px;
  }
}
</style>

