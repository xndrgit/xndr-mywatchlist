<template>
    <div>
        <h1>Home</h1>
        <MoviesListComponent v-for="movie in foundedMoviesGift" :key="movie.id" :movie="movie"/>

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

<style lang="scss" scoped></style>
