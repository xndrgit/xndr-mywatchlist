<template>
    <div class="container-fluid dark-mode">
        <div>
            <HeaderComponent :searchAllOldGift="searchAllOld" @searchAll="searchAllFunction" @update-data="updateData"/>
            <router-view :foundedMoviesGift="foundedMovies" :foundedPersonsGift="foundedPersons"
                         :foundedSeriesGift="foundedSeries"

                         :foundedTrendingMoviesGift="foundedTrendingMovies"
                         :foundedTrendingPersonsGift="foundedTrendingPersons"
                         :foundedTrendingSeriesGift="foundedTrendingSeries"

                         @nextMoviesPage="pageNextMoviesFunction"
                         @nextSeriesPage="pageNextSeriesFunction"

                         @nextTrendingMoviesPage="pageNextTrendingMoviesFunction"
                         @prevMoviesPage="pagePrevMoviesFunction"

                         @prevSeriesPage="pagePrevSeriesFunction"
                         @prevTrendingMoviesPage="pagePrevTrendingMoviesFunction"
            >
            </router-view>
            <FooterComponent/>
        </div>

    </div>
</template>


<script>
import axios from 'axios';

import HeaderComponent from "../components/HeaderComponent.vue";
import FooterComponent from "../components/FooterComponent.vue";

import HomePage from "../pages/HomePage.vue";


export default {
    name: 'App',
    computed: {
        // pc(){
        //     return window.innerWidth >= 768;
        // },
    },
    components: {
        FooterComponent,
        HeaderComponent,
        HomePage,
    },
    data: function () {
        return {
            // https://developers.themoviedb.org/3/search/search-movies
            apiKey: 'da54add692c53fb6bacfc3b15da91484',
            apiUrlMovie: 'https://api.themoviedb.org/3/search/movie',
            apiUrlTv: 'https://api.themoviedb.org/3/search/tv',
            apiUrlPerson: 'https://api.themoviedb.org/3/search/person',

            pageMovies: 1,
            pageSeries: 1,
            pagePersons: 1,

            pageTrendingMovies: 1,
            pageTrendingSeries: 1,
            pageTrendingPersons: 1,

            apiUrlTrendingMovie: 'https://api.themoviedb.org/3/trending/movie/day',
            apiUrlTrendingTv: 'https://api.themoviedb.org/3/trending/tv/day',
            apiUrlTrendingPerson: 'https://api.themoviedb.org/3/trending/person/day',

            searchAll: '',
            searchAllOld: [],

            // founded datas da passare a chi vuoi
            foundedMovies: [],
            foundedSeries: [],
            foundedPersons: [],

            foundedTrendingMovies: [],
            foundedTrendingSeries: [],
            foundedTrendingPersons: [],
        }
    },
    methods: {


        // stai salvando il risultato passato mediante la emit nella variabile searchMovies,
        // poi con getMovies richiami questa variabile, non necessaria, essendo che potresti passare il valore della emit direttamente alla funzione getMovies()
        searchAllFunction(result) {
            console.log(`App.vue is saying:  ${result}`);
            this.searchAll = result;
        },
        updateData(data) {
            this.foundedMovies = data.foundedMovies;
            this.foundedSeries = data.foundedSeries;
            this.foundedPersons = data.foundedPersons;
            console.log(`App.vue founded data edited`)
        },
        getMovies(wha) {
            axios.get(`${this.apiUrlMovie}?api_key=${this.apiKey}&query=${wha}&page=${this.pageMovies}`)
                .then((result) => {
                    // console.log(result);
                    this.foundedMovies = result.data.results;
                    console.log(`${this.apiUrlMovie}?api_key=${this.apiKey}&query=${wha}&page=${this.pageMovies}`);
                })
                .catch((error) => {
                    console.warn(error)
                })
        },
        getSeries(wha) {
            axios.get(`${this.apiUrlTv}?api_key=${this.apiKey}&query=${wha}&page=${this.pageSeries}`)
                .then((result) => {
                    // console.log(result);
                    this.foundedSeries = result.data.results;
                    console.log(this.foundedSeries);
                })
                .catch((error) => {
                    console.warn(error)
                })
        },
        getPersons(wha) {
            axios.get(`${this.apiUrlPerson}?api_key=${this.apiKey}&query=${wha}&page=${this.pagePersons}`)
                .then((result) => {
                    // console.log(result);
                    this.foundedPersons = result.data.results;
                    console.log(this.foundedPersons);
                })
                .catch((error) => {
                    console.warn(error)
                })
        },

        getTrendingMovies(wha) {
            axios.get(`${this.apiUrlTrendingMovie}?api_key=${this.apiKey}&page=${this.pageTrendingMovies}`)
                .then((result) => {
                    // console.log(result);
                    this.foundedTrendingMovies = result.data.results;
                })
                .catch((error) => {
                    console.warn(error);
                })
        },
        getTrendingSeries(wha) {
            axios.get(`${this.apiUrlTrendingTv}?api_key=${this.apiKey}&page=${this.pageTrendingSeries}`)
                .then((result) => {
                    // console.log(result);
                    this.foundedTrendingSeries = result.data.results;
                })
                .catch((error) => {
                    console.warn(error)
                })
        },
        getTrendingPersons(wha) {
            axios.get(`${this.apiUrlTrendingPerson}?api_key=${this.apiKey}&page=${this.pageTrendingPersons}`)
                .then((result) => {
                    this.foundedTrendingPersons = result.data.results;
                    console.log(this.foundedTrendingPersons);
                })
                .catch((error) => {
                    console.warn(error)
                })
        },
        pageNextMoviesFunction(page) {
            this.pageMovies = page;
            // console.log(this.pageMovies);
            this.getMovies(this.searchAll);
        },
        pagePrevMoviesFunction(page) {
            this.pageMovies = page;
            console.log(this.pageMovies);
            this.getMovies(this.searchAll);
            this.getTrendingMovies();
        },

        pageNextTrendingMoviesFunction(page) {
            this.pageTrendingMovies = page;
            // console.log(this.pageTrendingMovies);
            this.getTrendingMovies();
        },
        pagePrevTrendingMoviesFunction(page) {
            this.pageTrendingMovies = page;
            // console.log(this.pageTrendingMovies);
            this.getTrendingMovies();
        },


        pageNextSeriesFunction(page) {
            this.pageSeries = page;
            console.log(this.pageSeries);
            this.getSeries(this.searchAll);
            this.getTrendingSeries();
        },
        pagePrevSeriesFunction(page) {
            this.pageSeries = page;
            console.log(this.pageSeries);
            this.getSeries(this.searchAll);
            this.getTrendingSeries();
        }


    },
    watch: {
        // esegui tutte le volte che cambia il valore di searchMovies, richiami getMovies col newVal
        searchAll: function (newVal, oldVal) {

            this.page = 1;

            // Store the old value in a separate variable or array, if is not present in the array
            if (!this.searchAllOld.includes(newVal)) {
                this.searchAllOld.push(newVal);
            }


            // If searchAllOld has more than 15 items, remove the oldest item
            if (this.searchAllOld.length > 10) {
                this.searchAllOld.shift();
            }


            //! Save searchAllOld to Local Storage
            // localStorage.setItem(key, value) is a method that allows you to store data in the user's
            // browser using the Local Storage API. The key parameter is a string that represents the
            // name of the data you want to store, and the value parameter is the data itself.
            // In this case, we're using localStorage.setItem() to store the searchAllOld array in the browser's
            // Local Storage. We're using JSON.stringify() to convert the array into a string, since Local Storage
            // can only store strings.
            // JSON.stringify() is a method that converts a JavaScript object or array into a JSON string.
            // In this case, we're using it to convert the searchAllOld array into a JSON string that can be stored
            // in Local Storage.
            localStorage.setItem('searchAllOld', JSON.stringify(this.searchAllOld));
            console.log(localStorage);

            console.log(`📢 | old val: ${oldVal}`)
            console.log(`📢 | log: ${this.searchAllOld}`)

            this.getMovies(newVal);
            this.getSeries(newVal);
            this.getPersons(newVal);

        },
    },
    created() {
        this.getTrendingMovies();
        this.getTrendingSeries();
        this.getTrendingPersons();

        // Retrieve searchAllOld from Local Storage
        let searchAllOld = JSON.parse(localStorage.getItem('searchAllOld')) || [];
        this.searchAllOld = searchAllOld;
    },
}
</script>


<style lang="scss">
// Default styles for light mode
body {
    background: url("https://wallpapers.com/images/featured/movie-9pvmdtvz4cb0xl37.jpg");
    background-position: center;
    background-size: contain;

    color: #fff;
    //font-family: 'Josefin Slab', serif;
    font-family: 'VT323', monospace;
}

body::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 300%;
    background: rgba(0, 0, 0, 0.85); /* Black background with 50% opacity */
}

// Styles for dark mode
body.dark-mode {
    background-color: black;
    color: white;
}

// Additional styles for dark mode
body.dark-mode h1 {
    color: white;
}

body.dark-mode a {
    color: #aaf;
}

body.dark-mode .btn {
    background-color: #aaf;
    color: #333;
}

// Media query to enable dark mode at a certain screen width
@media (min-width: 768px) {
}

</style>
