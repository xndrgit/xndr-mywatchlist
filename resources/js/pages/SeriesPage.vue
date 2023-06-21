<template>
    <div class="container-lg">
        <div class="row">
            <div class="col-12 cards-netflix">
                <img v-if="!foundedSeriesGift.length > 0" :src="imagePath('trendingseries.png')"
                     alt="TrendingSeriesImage"
                     class="img-fluid title-list-trending">
                <SeriesListComponent v-for="tv in foundedTrendingSeriesGift" v-if="!foundedSeriesGift.length > 0"
                                     :key="tv.id" :tv="tv"/>
                <img v-if="foundedSeriesGift.length > 0" :src="imagePath('series.png')" alt="SeriesImage"
                     class="img-fluid title-list-trending">
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
