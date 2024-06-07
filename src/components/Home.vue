<template>
    <div class="home">
        <div class="overlay"></div>
        <div class="t">
            <h1 class="titre">Portfolio de Noam JOLY-GIRODS</h1>
            <p class="sous-titre">Gestion de demandes informatiques à la mairie de Montbéliard</p>
        </div>
    </div>
</template>

<script>
</script>

<style scoped>
h1 {
    font-size: 43px;
    color: white;
}

.home {
    width: 100%;
    height: 100vh;
    background-image: url('../assets/Mairie_de_Montbéliard.jpg');
    background-size:cover;
    background-position: center;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
}

.overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
}

.t {
    display: flex;
    flex-direction: column;
    align-items: center;
    z-index: 1;
}

.sous-titre {
    color: white;
    font-size: 16px;
    margin-top: 8px;
    font-weight: lighter;
}
</style>
