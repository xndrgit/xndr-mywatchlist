<template>
    <div class="container-lg">
        <div class="row">
            <div class="col-12 cards-netflix">
                <!--                <h1 class="col-12 text-center">ᴍᴏᴠɪᴇꜱ</h1>-->
                <MoviesListComponent v-for="movie in foundedMoviesGift" :key="movie.id" :movie="movie"/>
            </div>

            <div class="col-12 cards-netflix">
                <!--                <h1 class=" col-12 text-center">ꜱᴇʀɪᴇꜱ</h1>-->
                <SeriesListComponent v-for="tv in foundedSeriesGift" :key="tv.id" :tv="tv"/>
            </div>

            <div class="col-12 cards-netflix">

                <PersonsListComponent v-for="person in foundedPersonsGift" :key="person.id" :person="person"/>
            </div>


        </div>
    </div>
</template>

<script>
import MoviesListComponent from "../components/MoviesListComponent.vue";
import SeriesListComponent from "../components/SeriesListComponent.vue";
import PersonsListComponent from "../components/PersonsListComponent.vue";

export default {
    name: 'HomePage',
    mounted() {
        console.log('HomePage mounted.')
    },
    components: {
        MoviesListComponent,
        SeriesListComponent,
        PersonsListComponent
    },
    props: {
        foundedMoviesGift: Array,
        foundedSeriesGift: Array,
        foundedPersonsGift: Array,
    }
}
</script>

<style lang="scss" scoped>

.row {
    min-height: 80vh;

    .cards-netflix {
        min-height: 680px;

        display: flex;
        align-items: center;

        overflow-x: scroll;
        overflow-y: hidden;
        scrollbar-width: none; /* hide scrollbar for Firefox */

        //The white-space: nowrap property is used to prevent the cards from wrapping to the next line, which is necessary to keep them in a single row. If the cards were allowed to wrap, the horizontal scrolling would not work as expected.
        white-space: nowrap;
        flex-wrap: nowrap;
    }

    .cards-netflix::-webkit-scrollbar {
        display: none; /* hide scrollbar for Chrome, Safari, and Edge */
    }
}

</style>
