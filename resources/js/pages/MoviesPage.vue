<template>
    <div class="container-lg">
        <div class="row">
            <div class="col-12 mb-5 cards-netflix">
                <div class="col-12 d-flex justify-content-center mt-4">
                    <img v-if="!foundedMoviesGift.length > 0" :src="imagePath('trendingmovies.png')"
                         alt="TrendingMoviesImage"
                         class="img-fluid title-list-trending">
                </div>
                <MoviesListComponent v-for="movie in foundedTrendingMoviesGift" v-if="!foundedMoviesGift.length > 0"
                                     :key="movie.id" :movie="movie"/>
                <div class="col-12 d-flex justify-content-center mt-4">
                    <img v-if="foundedMoviesGift.length > 0" :src="imagePath('movies.png')" alt="MoviesImage"
                         class="img-fluid title-list-trending">
                </div>

                <MoviesListComponent v-for="movie in foundedMoviesGift" v-if="foundedMoviesGift.length > 0"
                                     :key="movie.id" :movie="movie"/>
            </div>
            <div class="col-12 d-flex justify-content-around my-2">
                <div>
                    <button>Prev</button>
                </div>
                <div>
                    <button>Next</button>
                </div>
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
            return require(`../../../public/assets/${filename}`);
        },
    }
}
</script>

<style lang="scss" scoped>

.row {
    min-height: 80vh;

    .title-list-trending {
        height: fit-content;
        width: 50%;


        background: black;
        padding: 4px 20px;

    }

    .cards-netflix {
        display: flex;
        flex-wrap: wrap;
    }
}

</style>
