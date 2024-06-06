<template>
    <nav :class="['navbar', { 'navbar-scrolled': isScrolled }]">
        <div class="logo">
            <img src="@/assets/logo.png" alt="Logo" class="logo-image"/>
        </div>
        <div class="nav-center">
            <ul class="nav-links">
                <li><a href="">Acceuil</a></li>
                <li><a href="">A propos</a></li>
                <li><a href="">Compétences</a></li>
                <li><a href="">Contexte</a></li>
                <li><a href="">Projet</a></li>
            </ul>
        </div>
    </nav>
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

        return {
            isScrolled
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
    background-color: #333;
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
