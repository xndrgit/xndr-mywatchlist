<template>
    <div class="container-lg dark-mode">

        <HeaderComponent @searchAll="searchAllFunction"/>
        <router-view :foundedMoviesGift="foundedMovies" :foundedPersonsGift="foundedPersons"
                     :foundedSeriesGift="foundedSeries"></router-view>
        <FooterComponent/>
    </div>
</template>


<script>
import axios from 'axios';

import HeaderComponent from "../components/HeaderComponent.vue";
import FooterComponent from "../components/FooterComponent.vue";

import HomePage from "../pages/HomePage.vue";


export default {
    name: 'App',
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

            searchAll: '',
            searchAllOld: [],

            // founded datas da passare a chi vuoi
            foundedMovies: [],
            foundedSeries: [],
            foundedPersons: [],
        }
    },
    methods: {
        // stai salvando il risultato passato mediante la emit nella variabile searchMovies,
        // poi con getMovies richiami questa variabile, non necessaria, essendo che potresti passare il valore della emit direttamente alla funzione getMovies()
        searchAllFunction(result) {
            console.log(`App.vue is saying:  ${result}`);
            this.searchAll = result;
        },
        getMovies(wha) {
            axios.get(`${this.apiUrlMovie}?api_key=${this.apiKey}&query=${wha}`)
                .then((result) => {
                    // console.log(result);
                    this.foundedMovies = result.data.results;
                    console.log(this.foundedMovies);
                })
                .catch((error) => {
                    console.warn(error)
                })
        },
        getSeries(wha) {
            axios.get(`${this.apiUrlTv}?api_key=${this.apiKey}&query=${wha}`)
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
            axios.get(`${this.apiUrlPerson}?api_key=${this.apiKey}&query=${wha}`)
                .then((result) => {
                    // console.log(result);
                    this.foundedPersons = result.data.results;
                    console.log(this.foundedPersons);
                })
                .catch((error) => {
                    console.warn(error)
                })
        },


    },
    watch: {
        // esegui tutte le volte che cambia il valore di searchMovies, richiami getMovies col newVal
        searchAll: function (newVal, oldVal) {

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
        }
    },

    created() {
        // Retrieve searchAllOld from Local Storage
        let searchAllOld = JSON.parse(localStorage.getItem('searchAllOld')) || [];
        this.searchAllOld = searchAllOld;
    },
}
</script>


<style lang="scss">
// Default styles for light mode
body {
    background-color: #343a40;
    color: #fff;
}

// Styles for dark mode
body.dark-mode {
    background-color: #343a40;
    color: #fff;
}

// Additional styles for dark mode
body.dark-mode h1 {
    color: #fff;
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
