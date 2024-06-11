<template>
    <nav :class="['navbar', { 'navbar-scrolled': isScrolled }]">
        <div class="logo" @click="launchConfetti">
            <img src="@/assets/logo.png" alt="Logo" class="logo-image"/>
        </div>
        <div class="nav-center">
            <ul class="nav-links">
                <li><a href="#accueil" @click.prevent="scrollToSection('accueil')">Accueil</a></li>
                <li><a href="#contexte" @click.prevent="scrollToSection('contexte')">Contexte</a></li>
                <li><a href="#langage" @click.prevent="scrollToSection('langage')">Technologies</a></li>
                <li><a href="#competence" @click.prevent="scrollToSection('competence')">Compétences</a></li>
                <li><a href="#projet" @click.prevent="scrollToSection('projet')">Projet</a></li>
                <li><a href="#contact" @click.prevent="scrollToSection('footer')">Contact</a></li>
            </ul>
        </div>
    </nav>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue';
import confetti from 'canvas-confetti';

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

        const launchConfetti = () => {
            confetti({
                particleCount: 100,
                spread: 70,
                origin: { y: 0.6 }
            });
        };

        return {
            isScrolled,
            scrollToSection,
            launchConfetti
        };
    }
};
</script>

<style scoped>
.logo {
    border-radius: 20px;
}

.navbar {
    background-color: transparent;
    color: #fff;
    height: 100px;
    position: fixed;
    width: 100%;
    display: flex;
    align-items: center;
    transition: background-color 0.3s ease;
    z-index: 2;
}

.navbar-scrolled {
    background-color: #252422;
}

.logo {
    position: absolute;
    left: 2rem;
    top: 50%;
    transform: translateY(-50%);
}

.logo-image {
    border-radius: 15px;
    height: 50px;
    transition: height 0.3s;
    cursor: pointer;
}

.nav-center {
    margin: 0 auto;
    text-align: center;
}

.nav-links {
    list-style: none;
    display: flex;
    margin: 0;
    padding: 0;
    gap: 2rem;
    justify-content: center;
}

.nav-links li a {
    color: #fff;
    text-decoration: none;
    font-size: 1.1rem;
}

.nav-links li a:hover {
    text-decoration: underline;
}
</style>
