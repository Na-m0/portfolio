<script setup>
import NavBar from './components/NavBar.vue';
import FooTer from './components/FooTer.vue';
import Competence from './components/Competence.vue';
import Contexte from './components/Contexte.vue';
import Projet from './components/Projet.vue';
import Home from "@/components/Home.vue";
import Langage from "@/components/Langage.vue";

</script>

<template>
    <div>
      <NavBar/>
        <div id="accueil">
            <Home/>
        </div>
        <div id="contexte" class="content">
          <Contexte/>
        </div>
        <div id="langage" class="content">
          <Langage/>
        </div>
        <div id="competence" class="content">
          <Competence/>
        </div>
        <div id="projet" class="content-projet">
          <Projet/>
        </div>
        <div id="footer">
            <FooTer/>
        </div>
    </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500;600;700;800;900&display=swap");

h1 {
  font-size: 37px;
}

h2 {
  font-size: 25px;
}

h3 {
  font-size: 18px;
}

p {
  font-size: 20px;
  font-weight: normal;
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
    position: relative; 
    z-index: 1;
}
.content-projet {
  position: relative; 
  z-index: 0;
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
