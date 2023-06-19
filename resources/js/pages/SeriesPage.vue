<template>
    <div class="container-lg">
        <div class="row">
            <div class="col-12 cards-netflix">
                <SeriesListComponent v-for="tv in foundedTrendingSeriesGift" v-if="!foundedSeriesGift.length > 0"
                                     :key="tv.id" :tv="tv"/>
                <SeriesListComponent v-for="tv in foundedSeriesGift" v-if="foundedSeriesGift.length > 0" :key="tv.id"
                                     :tv="tv"/>
            </div>
        </div>
    </div>
</template>

<script>
import SeriesListComponent from "../components/SeriesListComponent.vue";

export default {
    name: 'SeriesPage',
    mounted() {
        console.log('SeriesPage mounted.')
    },
    components: {
        SeriesListComponent,
    },
    props: {
        foundedSeriesGift: Array,
        foundedTrendingSeriesGift: Array,
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
