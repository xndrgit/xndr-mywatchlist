<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-12 mb-5 cards-netflix justify-content-between">
                <div class="col-12 d-flex justify-content-center">
                    <img v-if="!foundedSeriesGift.length > 0" :src="imagePath('trendingseries.png')"
                         alt="TrendingSeriesImage"
                         class="img-fluid title-list-trending">
                </div>
                <SeriesListComponent v-for="tv in foundedTrendingSeriesGift" v-if="!foundedSeriesGift.length > 0"
                                     :key="tv.id" :tv="tv"/>
                <div class="col-12 d-flex justify-content-center">
                    <div v-if="foundedSeriesGift.length > 0" class="col-12 d-flex justify-content-center">
                    <span class="title-list-founded">
                        Founded Series

                       <i class="fa-solid fa-check fa-bounce" style="color: #37ff00;"></i>
                    </span>

                    </div>
                    <!--                    <img v-if="foundedSeriesGift.length > 0" :src="imagePath('series.png')" alt="SeriesImage"-->
                    <!--                         class="img-fluid title-list-trending">-->
                </div>

                <SeriesListComponent v-for="tv in foundedSeriesGift" v-if="foundedSeriesGift.length > 0" :key="tv.id"
                                     :tv="tv"/>
            </div>
            <div class="col-12 d-flex justify-content-around my-5">
                <div>
                    <button @click="prevSeriesFunction">Prev</button>
                </div>
                <div>
                    {{ this.pageSeries }}
                </div>
                <div>
                    <button @click="nextSeriesFunction">Next</button>
                </div>
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
    data: function () {
        return {
            pageSeries: 1,
        }
    },
    methods: {
        imagePath(filename) {
            return require(`../../../public/assets/${filename}`);
        },
        nextSeriesFunction() {
            this.pageSeries = this.pageSeries + 1;
            this.$emit('nextSeriesPage', this.pageSeries);
        },
        prevSeriesFunction() {
            this.pageSeries = this.pageSeries - 1;
            this.$emit('prevSeriesPage', this.pageSeries);
        }
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
