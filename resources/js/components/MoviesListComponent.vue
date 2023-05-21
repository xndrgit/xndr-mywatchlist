<template>
        <MovieCardComponent :movie="movie"/>
</template>

<script>
import MovieCardComponent from "./MovieCardComponent.vue";

export default {
    mounted() {
    },
    props: {
        movie: {
            type: Object,
            required: true,
        }
    },
    components: {
        MovieCardComponent,
    },
}
</script>

<style lang="scss" scoped>
</style>
