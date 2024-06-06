<script setup>
import NavBar from './components/NavBar.vue';
import FooTer from './components/FooTer.vue';
import About from './components/About.vue';
import Contexte from './components/Contexte.vue';
import Projet from './components/Projet.vue';
</script>

<template>
  <div>
    <NavBar/>
    <div class="content">
      <About/>
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
  height: 300px;
  margin: 1% auto;
  background-color: #f0f0f0; 
  border-radius: 20px; 
  display: flex;
  align-items: center; 
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
  padding: 1rem;
  padding-top: 700px;
  background-color: #a97441b5;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
