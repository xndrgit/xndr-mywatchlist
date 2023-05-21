<template>
    <div>
        <h1>Home</h1>
        <div class="cards-netflix">
            <MoviesListComponent v-for="movie in foundedMoviesGift" :key="movie.id" :movie="movie"/>
        </div>
    </div>
</template>

<script>
import MoviesListComponent from "../components/MoviesListComponent.vue";

export default {
    name: 'HomePage',
    mounted() {
        console.log('HomePage mounted.')
    },
    components: {
        MoviesListComponent,
    },
    props: {
        foundedMoviesGift: Array,
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
