<template>
    <nav :class="['navbar', { 'navbar-scrolled': isScrolled }]">
      <div class="logo">
        <img src="@/assets/logo.png" alt="Logo" class="logo-image"/>
      </div>
      <div class="nav-center">
        <ul class="nav-links">
          <li><a href="#home">Home</a></li>
          <li><a href="#about">A propos</a></li>
          <li><a href="#services">Context</a></li>
          <li><a href="#contact">Projet</a></li>
        </ul>
        <div v-if="!isScrolled" class="title">
          Noam JOLY-GIRODS
        </div>
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
  .navbar {
    background-color: #333;
    color: #fff;
    height: 600px;
    padding: 1rem 0;
    position: fixed;
    width: 100%;
    top: 0;
    left: 0;
    transition: height 0.3s, padding 0.3s;
    z-index: 1000;
    display: flex;
    align-items: center;
  }
  
  .navbar-scrolled {
    height: 60px;
    padding: 0.5rem 0;
  }
  
  .logo {
    position: absolute;
    left: 2rem;
    top: 50%;
    transform: translateY(-50%);
  }
  
  .logo-image {
    height: 50px;
    transition: height 0.3s;
  }
  
  .navbar-scrolled .logo-image {
    height: 30px;
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
  
  .title {
    font-size: 1.5rem;
    margin-top: 0.5rem;
    color: #fff;
  }
  
  .nav {
    margin: 0 auto;
  }
  </style>
  