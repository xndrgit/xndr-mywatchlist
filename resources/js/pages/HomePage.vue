<template>
    <div class="container-lg">
        <div class="row flex-column">


            <div v-if="!foundedMoviesGift.length > 0" class="position-relative">
                <img :src="imagePath('trendingmovies.png')" alt="TrendingMoviesImage"
                     class="img-fluid title-list-trending">
                <!--                The ref attribute is used to create a reference to the cardsContainerMovie element, which is used by -->
                <!--                the scrollCardsMovie method to scroll the movies list container.-->
                <div ref="cardsContainerMovie" class="col-12 cards-netflix">

                    <!--                <h1 class="col-12 text-center">ᴍᴏᴠɪᴇꜱ</h1>-->
                    <MoviesListComponent v-for="movie in foundedTrendingMoviesGift" :key="movie.id" :movie="movie"/>
                </div>
                <div class="arrows">
                    <div class="next p-3 bg-white rounded-circle" @click="scrollCardsMovie('next')">
                    </div>
                    <div class="prev p-3 bg-white rounded-circle" @click="scrollCardsMovie('prev')">
                    </div>
                </div>
            </div>
            <!-- The position-relative class is used to set the positioning context for the movies list and arrow buttons.-->
            <div v-if="foundedMoviesGift.length > 0" class="position-relative">
                <img v-if="foundedMoviesGift.length > 0" :src="imagePath('movies.png')" alt="MoviesImage"
                     class="img-fluid title-list">

                <!--                The ref attribute is used to create a reference to the cardsContainerMovie element, which is used by -->
                <!--                The scrollCardsMovie method to scroll the movies list container.-->
                <div ref="cardsContainerMovie" class="col-12 cards-netflix">

                    <!--                <h1 class="col-12 text-center">ᴍᴏᴠɪᴇꜱ</h1>-->
                    <MoviesListComponent v-for="movie in foundedMoviesGift" :key="movie.id" :movie="movie"/>
                </div>
                <div class="arrows">
                    <div class="next p-3 bg-white rounded-circle" @click="scrollCardsMovie('next')">
                    </div>
                    <div class="prev p-3 bg-white rounded-circle" @click="scrollCardsMovie('prev')">
                    </div>
                </div>
            </div>

            <div v-if="!foundedSeriesGift.length > 0" class="position-relative">
                <img :src="imagePath('trendingseries.png')" alt="TrendingSeriesImage"
                     class="img-fluid title-list-trending">
                <div ref="cardsContainerTv" class="col-12 cards-netflix">
                    <!--                <h1 class=" col-12 text-center">ꜱᴇʀɪᴇꜱ</h1>-->
                    <SeriesListComponent v-for="tv in foundedTrendingSeriesGift" :key="tv.id" :tv="tv"/>
                </div>
                <div class="arrows">
                    <div class="next p-3 bg-white rounded-circle" @click="scrollCardsTv('next')">
                    </div>
                    <div class="prev p-3 bg-white rounded-circle" @click="scrollCardsTv('prev')">
                    </div>
                </div>
            </div>
            <div v-if="foundedSeriesGift.length > 0" class="position-relative">
                <img v-if="foundedSeriesGift.length > 0" :src="imagePath('series.png')" alt="SeriesImage"
                     class="img-fluid title-list">
                <div ref="cardsContainerTv" class="col-12 cards-netflix">
                    <!--                <h1 class=" col-12 text-center">ꜱᴇʀɪᴇꜱ</h1>-->
                    <SeriesListComponent v-for="tv in foundedSeriesGift" :key="tv.id" :tv="tv"/>
                </div>
                <div class="arrows">
                    <div class="next p-3 bg-white rounded-circle" @click="scrollCardsTv('next')">
                    </div>
                    <div class="prev p-3 bg-white rounded-circle" @click="scrollCardsTv('prev')">
                    </div>
                </div>
            </div>

            <div v-if="!foundedPersonsGift.length > 0" class="position-relative">
                <img :src="imagePath('trendingpersons.png')" alt="TrendingPersonsImage"
                     class="img-fluid title-list-trending">
                <div ref="cardsContainerPerson" class="col-12 cards-netflix">
                    <PersonsListComponent v-for="person in foundedTrendingPersonsGift" v-if="person" :key="person.id"
                                          :person="person"/>
                </div>
                <div class="arrows">
                    <div class="next p-3 bg-white rounded-circle" @click="scrollCardsPersons('next')">
                    </div>
                    <div class="prev p-3 bg-white rounded-circle" @click="scrollCardsPersons('prev')">
                    </div>
                </div>
            </div>
            <div v-if="foundedPersonsGift.length > 0" class="position-relative">
                <img v-if="foundedPersonsGift.length > 0" :src="imagePath('persons.png')" alt="PersonsImage"
                     class="img-fluid title-list">
                <div ref="cardsContainerPerson" class="col-12 cards-netflix">
                    <PersonsListComponent v-for="person in foundedPersonsGift" v-if="person" :key="person.id"
                                          :person="person"/>
                </div>
                <div class="arrows">
                    <div class="next p-3 bg-white rounded-circle" @click="scrollCardsPersons('next')">
                    </div>
                    <div class="prev p-3 bg-white rounded-circle" @click="scrollCardsPersons('prev')">
                    </div>
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
    data: function () {
        return {}
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

        foundedTrendingMoviesGift: Array,
        foundedTrendingSeriesGift: Array,
        foundedTrendingPersonsGift: Array,

    },
    methods: {
        imagePath(filename) {
            return require(`../../../public/assets/${filename}`);
        },

        scrollCardsMovie(direction) {
            // Retrieve a reference to the cards container element using `$refs`
            const cardsContainerMovie = this.$refs.cardsContainerMovie;

            // Calculate the width of a card by querying for the first element with the class "card"
            const cardWidth = cardsContainerMovie.querySelector('.card').offsetWidth;

            // Retrieve the current scroll position of the cards container element
            const currentScrollPos = cardsContainerMovie.scrollLeft;

            this.isAtStartMovie = cardsContainerMovie.scrollLeft === 0;
            this.isAtEndMovie = cardsContainerMovie.scrollLeft + cardsContainerMovie.offsetWidth === cardsContainerMovie.scrollWidth;

            // Calculate the new scroll position based on the direction passed in as an argument
            let newScrollPos;
            if (direction === 'next') {
                newScrollPos = currentScrollPos + (cardWidth * 3);
            } else if (direction === 'prev') {
                newScrollPos = currentScrollPos - (cardWidth * 3);
            }

            // Scroll the cards container element to the new position with a smooth animation
            cardsContainerMovie.scrollTo({
                left: newScrollPos,
                behavior: 'smooth'
            });
        },
        scrollCardsTv(direction) {
            // Retrieve a reference to the cards container element using `$refs`
            const cardsContainerTv = this.$refs.cardsContainerTv;

            // Calculate the width of a card by querying for the first element with the class "card"
            const cardWidth = cardsContainerTv.querySelector('.card').offsetWidth;

            // Retrieve the current scroll position of the cards container element
            const currentScrollPos = cardsContainerTv.scrollLeft;

            // Calculate the new scroll position based on the direction passed in as an argument
            let newScrollPos;
            if (direction === 'next') {
                newScrollPos = currentScrollPos + (cardWidth * 3);
            } else if (direction === 'prev') {
                newScrollPos = currentScrollPos - (cardWidth * 3);
            }

            // Scroll the cards container element to the new position with a smooth animation
            cardsContainerTv.scrollTo({
                left: newScrollPos,
                behavior: 'smooth'
            });
        },
        scrollCardsPersons(direction) {
            const cardsContainerPersons = this.$refs.cardsContainerPerson;
            const cardWidth = cardsContainerPersons.querySelector('.card').offsetWidth;
            const currentPosition = cardsContainerPersons.scrollLeft;

            let newPosition;
            if (direction === 'next') {
                newPosition = currentPosition + (cardWidth * 3);
            } else if (direction === 'prev') {
                newPosition = currentPosition - (cardWidth * 3);
            }

            cardsContainerPersons.scrollTo({
                left: newPosition,
                behavior: "smooth"
            });
        },
    },
}
</script>

<style lang="scss" scoped>


.row {
    min-height: 80vh;

    .title-list {
        position: absolute;
        top: 20px;
        width: 25%;

        border: 1px solid rgba(39, 39, 39, 1);
        background: black;
        padding: 4px 20px;
        border-radius: 25px;

        left: 50%;
        transform: translateX(-50%);

        z-index: 10;
    }

    .title-list-trending {
        position: absolute;
        top: 20px;
        width: 25%;

        border: 1px solid rgba(39, 39, 39, 1);
        background: black;
        padding: 4px 20px;
        border-radius: 25px;

        left: 50%;
        transform: translateX(-50%);

        z-index: 10;
    }

    .prev {
        opacity: 0;

        position: absolute;
        left: -40px;
        bottom: 35%;

        z-index: 999999999999999999;

        transition: opacity 0.5s ease-in-out; /* Add transition */

    }

    .next {
        opacity: 0;

        position: absolute;
        right: -40px;
        bottom: 35%;

        z-index: 999999999999999999;

        transition: opacity 0.2s ease-in-out; /* Add transition */
    }


    .position-relative:hover .prev, .position-relative:hover .next {

        opacity: 0.6; /* Change opacity on hover of .cards-netflix */
    }


    .cards-netflix {

        min-height: 460px;

        display: flex;
        align-items: flex-end;

        overflow-x: scroll;
        overflow-y: hidden;
        scrollbar-width: none; /* hide scrollbar for Firefox */

        //The white-space: nowrap property is used to prevent the cards from wrapping to the next line, which is necessary to keep them in a single row. If the cards were allowed to wrap, the horizontal scrolling would not work as expected.
        white-space: nowrap;
        flex-wrap: nowrap;

        //background-image: url(https://media.tenor.com/BOu8ryjIR38AAAAC/sound-wave-wave.gif);
        background-repeat: no-repeat;
        background-position-x: center;
        background-position-y: center;
        background-size: cover;


    }

    .cards-netflix::-webkit-scrollbar {
        display: none; /* hide scrollbar for Chrome, Safari, and Edge */
    }


}


</style>
