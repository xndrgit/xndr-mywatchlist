<template>
    <div class="container-lg">
        <div class="row">
            <div class="position-relative">
                <div class="col-12 cards-netflix">
                    <!--                <h1 class="col-12 text-center">ᴍᴏᴠɪᴇꜱ</h1>-->
                    <MoviesListComponent v-for="movie in foundedMoviesGift" :key="movie.id" :movie="movie"/>
                </div>
                <div class="arrows">
                    <div class="next p-3 bg-white rounded-circle">
                    </div>
                    <div class="prev p-3 bg-white rounded-circle">
                    </div>
                </div>
            </div>

            <div class="position-relative">
                <div class="col-12 cards-netflix">
                    <!--                <h1 class=" col-12 text-center">ꜱᴇʀɪᴇꜱ</h1>-->
                    <SeriesListComponent v-for="tv in foundedSeriesGift" :key="tv.id" :tv="tv"/>
                </div>
            </div>

            <div class="position-relative">
                <div class="col-12 cards-netflix">

                    <PersonsListComponent v-for="person in foundedPersonsGift" :key="person.id" :person="person"/>
                </div>
            </div>


        </div>
    </div>
</template>

<script>
import MoviesListComponent from "../components/MoviesListComponent.vue";
import SeriesListComponent from "../components/SeriesListComponent.vue";
import PersonsListComponent from "../components/PersonsListComponent.vue";

export default {
    name: 'HomePage',
    mounted() {
        console.log('HomePage mounted.')
    },
    components: {
        MoviesListComponent,
        SeriesListComponent,
        PersonsListComponent
    },
    props: {
        foundedMoviesGift: Array,
        foundedSeriesGift: Array,
        foundedPersonsGift: Array,
    },
    methods: {
        scrollCards(direction) {
            const cardsContainer = this.$refs.cardsContainer;
            const cardWidth = cardsContainer.querySelector('.card').offsetWidth;
            const currentScrollPos = cardsContainer.scrollLeft;
            let newScrollPos;

            if (direction === 'next') {
                newScrollPos = currentScrollPos + cardWidth;
            } else if (direction === 'prev') {
                newScrollPos = currentScrollPos - cardWidth;
            }

            cardsContainer.scrollTo({
                left: newScrollPos,
                behavior: 'smooth'
            });
        }

    }
}
</script>

<style lang="scss" scoped>


.row {
    min-height: 80vh;

    .prev {
        opacity: 0;

        position: absolute;
        left: -40px;
        bottom: 45%;

        z-index: 999999999999999999;

        transition: opacity 0.5s ease-in-out; /* Add transition */

    }

    .next {
        opacity: 0;

        position: absolute;
        right: -40px;
        bottom: 45%;

        z-index: 999999999999999999;

        transition: opacity 0.2s ease-in-out; /* Add transition */
    }


    .position-relative:hover .prev, .position-relative:hover .next {
        opacity: 1; /* Change opacity on hover of .cards-netflix */
    }


    .cards-netflix {

        min-height: 680px;

        display: flex;
        align-items: center;

        overflow-x: scroll;
        overflow-y: hidden;
        scrollbar-width: none; /* hide scrollbar for Firefox */

        //The white-space: nowrap property is used to prevent the cards from wrapping to the next line, which is necessary to keep them in a single row. If the cards were allowed to wrap, the horizontal scrolling would not work as expected.
        white-space: nowrap;
        flex-wrap: nowrap;
    }

    .cards-netflix::-webkit-scrollbar {
        display: none; /* hide scrollbar for Chrome, Safari, and Edge */
    }


}


</style>
