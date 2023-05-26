<template>
    <div class="container-lg">
        <div class="row">
            <div class="col-12 cards-netflix">
                <!--                <h1 class=" col-12 text-center">ᴍᴏᴠɪᴇꜱ</h1>-->
                <MoviesListComponent v-for="movie in foundedMoviesGift" :key="movie.id" :movie="movie"/>
                <!--                <h1 class=" col-12 text-center">ꜱᴇʀɪᴇꜱ</h1>-->
                <SeriesListComponent v-for="tv in foundedSeriesGift" :key="tv.id" :tv="tv"/>

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
        display: flex;
        flex-wrap: wrap;
    }
}

</style>
