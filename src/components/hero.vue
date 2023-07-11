<template>
    <div class="hero">
        <div class="hero-text">
            <h2>Title</h2>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque volutpat orci ac mi maximus, id malesuada ante interdum.</p>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque volutpat orci ac mi maximus, id malesuada ante interdum.
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque volutpat orci ac mi maximus, id malesuada ante interdum.
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque volutpat orci ac mi maximus, id malesuada ante interdum.
            </p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'heroComponent'
}

</script>

<style scoped>
    .hero {
        display: flex;
        justify-content: flex-end;
        margin-top: 2%;
        margin-bottom: 5%;
        font-size: 1.3em;
        background-image: url("../assets/bilder/tai-s-captures-azwmrA7bdyM-unsplash-kopia.jpg");
        background-size: cover;
        background-repeat: no-repeat;
        min-height: 90vh;
    }

    .hero-text {
        display: flex;
        flex-direction: column;
        justify-content: center;
        width: 35%;
        margin: 0% 8% 0% 0%;
        padding: 2.5%;
        background-image: radial-gradient(circle, rgb(36, 36, 36), black);
        align-self: stretch;
        text-shadow: 2px 2px #000;
    }

    @media screen and (max-width: 1024px) {
        .hero-img {
            max-width: 30%;
        }
    }
    @media only screen and (max-width: 750px) {
        .hero {
            background-attachment: fixed;
        }
        .hero-text {
            width: 100%;
            padding: 0% 2% 0% 2%;
            align-self: flex-start;
            margin: 10% 0% 0% 0%;
        }
    }
</style>