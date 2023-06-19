<template>
    <div class="container-lg">
        <div class="row">
            <div class="col-12 cards-netflix">
                <MoviesListComponent v-for="movie in foundedTrendingMoviesGift" v-if="!foundedMoviesGift.length > 0"
                                     :key="movie.id" :movie="movie"/>
                <MoviesListComponent v-for="movie in foundedMoviesGift" v-if="foundedMoviesGift.length > 0"
                                     :key="movie.id" :movie="movie"/>
            </div>
        </div>
    </div>
</template>

<script>
import MoviesListComponent from "../components/MoviesListComponent.vue";

export default {
    name: 'MoviesPage',
    mounted() {
        console.log('MoviesPage mounted.')
    },
    components: {
        MoviesListComponent,
    },
    props: {
        foundedMoviesGift: Array,
        foundedTrendingMoviesGift: Array,
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
