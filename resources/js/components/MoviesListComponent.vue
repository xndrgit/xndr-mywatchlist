<template>
        <StandardCardComponent :item="movie"/>
</template>

<script>
import StandardCardComponent from "./StandardCardComponent.vue";

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
        StandardCardComponent,
    },
}
</script>

<style lang="scss" scoped>
</style>
