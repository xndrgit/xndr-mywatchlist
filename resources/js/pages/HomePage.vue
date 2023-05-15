<template>
    <div>
        <h1>Home</h1>
        {{ searchMoviesGift }}
    </div>
</template>

<script>
export default {
    name: 'HomePage',
    mounted() {
        console.log('HomePage mounted.')
    },
    props: {
        searchMoviesGift: String,
    }
}
</script>

<style lang="scss" scoped></style>
