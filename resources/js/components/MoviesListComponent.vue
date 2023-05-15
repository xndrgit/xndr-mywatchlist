<template>
    <div>
        {{ movie.title }}
    </div>
</template>

<script>
export default {
    mounted() {
    },
    props: {
        movie: {
            type: Object,
            required: true,
        }
    }
}
</script>

<style lang="scss" scoped>
</style>
