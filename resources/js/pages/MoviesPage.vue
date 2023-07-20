<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-12 mb-5 cards-netflix justify-content-between">
                <div class="col-12 d-flex justify-content-center">
                    <img v-if="!foundedMoviesGift.length > 0" :src="imagePath('trendingmovies.png')"
                         alt="TrendingMoviesImage"
                         class="img-fluid title-list-trending">
                </div>
                <MoviesListComponent v-for="movie in foundedTrendingMoviesGift" v-if="!foundedMoviesGift.length > 0"
                                     class=""
                                     :key="movie.id" :movie="movie"/>

                <div v-if="foundedMoviesGift.length > 0" class="col-12 d-flex justify-content-center">
                    <span class="title-list-founded">
                        Founded Movies
                       <i class="fa-solid fa-check fa-bounce" style="color: #37ff00;"></i>
                    </span>

                </div>
                <!--                <img v-if="foundedMoviesGift.length > 0" :src="imagePath('movies.png')" alt="MoviesImage"-->
                <!--                     class="img-fluid title-list-trending">-->

                <MoviesListComponent v-for="movie in foundedMoviesGift" v-if="foundedMoviesGift.length > 0"
                                     :key="movie.id" :movie="movie"/>
            </div>
            <div class="col-12 d-flex justify-content-around my-5">
                <div>
                    <button @click="prevMoviesFunction">Prev</button>
                </div>
                <div>
                    <div v-if="foundedMoviesGift.length > 0">
                        {{ this.pageMovies }}
                    </div>
                    <div v-if="!foundedMoviesGift.length > 0">
                        {{ this.pageTrendingMovies }}
                    </div>

                </div>
                <div>
                    <button @click="nextMoviesFunction">Next</button>
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
    data: function () {
        return {
            pageMovies: 1,
            pageTrendingMovies: 1,
        }
    },
    methods: {
        imagePath(filename) {
            return require(`../../../public/assets/${filename}`);
        },
        nextMoviesFunction() {

            if (this.foundedMoviesGift.length > 0) {
                this.pageMovies = this.pageMovies + 1;
                this.$emit('nextMoviesPage', this.pageMovies);
            } else {
                this.pageTrendingMovies = this.pageTrendingMovies + 1;
                this.$emit('nextTrendingMoviesPage', this.pageTrendingMovies);
            }


        },
        prevMoviesFunction() {

            if (this.foundedMoviesGift.length > 0) {
                this.pageMovies = this.pageMovies - 1;
                this.$emit('prevMoviesPage', this.pageMovies);
            } else {
                if (this.pageTrendingMovies > 1) {
                    this.pageTrendingMovies = this.pageTrendingMovies - 1;
                    this.$emit('prevTrendingMoviesPage', this.pageTrendingMovies);
                }
            }


        },
    }
}
</script>

<style lang="scss" scoped>

.row {
    min-height: 80vh;

    .title-list-trending {
        height: fit-content;
        width: 80vw;

    }

    .title-list-founded {
        color: #2eff00;
    }

    .cards-netflix {
        display: flex;
        flex-wrap: wrap;
    }
}

</style>
