<script setup>
import NavBar from './components/NavBar.vue';
import FooTer from './components/FooTer.vue';
import Competence from './components/Competence.vue';
import About from './components/About.vue';
import Contexte from './components/Contexte.vue';
import Projet from './components/Projet.vue';
import Home from "@/components/Home.vue";

</script>

<template>
    <div>
      <NavBar/>
      <Home/>
      <div class="content">
          <About/>
          <Competence/>
          <Contexte/>
          <Projet/>
      </div>
      <FooTer/>
    </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500;600;700;800;900&display=swap");

.container-top {
  width: 95%;
  height: 100%;
  margin: 1% auto;
  background-color: #f0f0f0;
  border-radius: 20px;
  display: flex;
  justify-content: center;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}

::-webkit-scrollbar {
  width: 0px;
  background: transparent;
}

header {
  line-height: 1.5;
}

.content {
    padding: 7rem;
    background-color: rgb(114, 110, 110);
    position: relative; /* Assurez-vous que le contenu est positionné pour les éléments absolus à l'intérieur */
    z-index: 1; /* Assurez-vous qu'il est en dessous de la barre de navigation */
}
@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
