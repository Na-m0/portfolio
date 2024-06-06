<template>
    <div class="container-top">
        <h1>Compétences</h1>
        <a>Voici les compétences qui doivent être validées lors de la deuxième année de BUT Informatique.</a>
        <div class="images-container">
            <img src="../assets/competence1.png" alt="Image 1" class="image-left">
            <img src="../assets/competence2.png" alt="Image 2" class="image-right">
        </div>
    </div>
</template>

<script>
</script>

<style scoped>
.container-top {
    display: flex;
    flex-direction: column;
    align-items: center;
}

a {
    font-size: 10px;
    margin: 40px;
}

.images-container {
    display: flex;
    justify-content: center;
    width: 100%;
    margin-bottom: 30px;
}

.image-left,
.image-right {
    width: 45%;
    border-radius: 20px;
    margin: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);

}
</style>
