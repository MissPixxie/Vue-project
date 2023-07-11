<template>
    <div class="cards">
        <h2>{{ title }}</h2>
        <p>{{ text }}</p>
    </div>
</template>

<script>

    export default {
        name: 'cardsKomponent',
        props: {
            title: String,
            text: String
        }
    }
</script>

<style scoped>
    .cards {
        display: flex;
        flex-direction: column;
        padding: 1%;
        width: 20%;
        background-image: linear-gradient(rgb(36, 36, 36), black);
        border-radius: 20px;
        box-shadow: 0px 3px 20px 2px rgba(0, 0, 0, 0.589);
        margin-bottom: 5%;
        font-size: 1.2em;
    }

    @media only screen and (max-width: 1024px) {
        .cards {
            width: 30%;
        }
    }
    @media only screen and (max-width: 750px) {
        .cards {
            width: 90%;
            padding: 0% 3% 0% 3%;
        }
    }
</style>