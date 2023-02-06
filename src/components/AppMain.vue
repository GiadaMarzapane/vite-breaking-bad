<script>

    export default {
        name: 'AppMain',
        props: {
            cardList: {
                type: Array,
                default: []
            }
        }
    }
</script>

<template>

    <main class="min-vh-100 py-4">

        <div class="container">
            <div class="row">
                <div class="col-auto mb-3">
                    <select name="archetype" id="archetype">
                        <option value="alien">Alien</option>
                    </select>
                </div>
            </div>
            <div class="row my-card-container py-3 px-4 g-2">
                <div class="single-card text-center col-3 pb-2" v-for="element in cardList">
                    <img :src="element.card_images[0].image_url_small" :alt="element.name">
                    <h5 class="text-white text-uppercase">
                        {{ element.name }}
                    </h5>
                    <span> {{ element.archetype }}</span>
                </div>
            </div>
        </div>

    </main>

</template>

<style lang="scss" scoped>
@use '../styles/main.scss' as *;

    main{
        background-color: $my-primary-color;
    }
    div.my-card-container{
        background-color: white;
    }
    div.single-card{
        background-color: $my-primary-color;
        img{
            height: 40vh;
        }
    }
</style>