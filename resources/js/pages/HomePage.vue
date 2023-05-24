<template>
    <div>
        <h6>Home</h6>
        <div class="cards-netflix">
            <h1 class="w-100">Movies</h1>
            <MoviesListComponent v-for="movie in foundedMoviesGift" :key="movie.id" :movie="movie"/>
        </div>
        <div class="cards-netflix">
            <h1 class="w-100">Series</h1>
            <SeriesListComponent v-for="tv in foundedSeriesGift" :key="tv.id" :tv="tv"/>
        </div>

    </div>
</template>

<script>
import MoviesListComponent from "../components/MoviesListComponent.vue";
import SeriesListComponent from "../components/SeriesListComponent.vue";

export default {
    name: 'HomePage',
    mounted() {
        console.log('HomePage mounted.')
    },
    components: {
        MoviesListComponent,
        SeriesListComponent,
    },
    props: {
        foundedMoviesGift: Array,
        foundedSeriesGift: Array,
    }
}
</script>

<style lang="scss" scoped>
.cards-netflix {

    display: flex;
    justify-content: space-between;

    overflow: hidden;
    flex-wrap: wrap;

}
</style>
