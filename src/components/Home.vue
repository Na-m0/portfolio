<template>
    <div class="home">
        <div class="overlay"></div>
        <div class="t">
            <a class="titre">Noam JOLY-GIRODS</a>
            <a class="sous-titre">2ème année d'étude en BUT Informatique</a>
        </div>
    </div>
</template>

<script>
</script>

<style scoped>
.home {
    width: 100%;
    height: 700px;
    background-image: url('src/assets/pexels-dreamlensproduction-1775777.jpg');
    background-size: cover;
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

.titre {
    color: white;
    font-size: 24px;
}

.sous-titre {
    color: white;
    font-size: 16px;
    margin-top: 8px;
}
</style>
