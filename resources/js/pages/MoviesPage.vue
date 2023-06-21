<template>
    <div class="container-lg">
        <div class="row">
            <div class="col-12 cards-netflix">
                <img v-if="!foundedMoviesGift.length > 0" :src="imagePath('trendingmovies.png')"
                     alt="TrendingMoviesImage"
                     class="img-fluid title-list-trending">
                <MoviesListComponent v-for="movie in foundedTrendingMoviesGift" v-if="!foundedMoviesGift.length > 0"
                                     :key="movie.id" :movie="movie"/>
                <img v-if="foundedMoviesGift.length > 0" :src="imagePath('movies.png')" alt="MoviesImage"
                     class="img-fluid title-list-trending">
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
    },
    methods: {
        imagePath(filename) {
            return require(`../../../public/images/${filename}`);
        },
    }
}
</script>

<style lang="scss" scoped>

.row {
    min-height: 80vh;

    .title-list-trending {
        height: fit-content;
        width: fit-content;
        padding: 1rem 10rem;
    }

    .cards-netflix {
        display: flex;
        flex-wrap: wrap;
    }
}

</style>
