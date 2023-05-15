<template>
    <div class="container-lg dark-mode">

        <HeaderComponent @searchMovies="searchMoviesFunction"/>
        <router-view :foundedMoviesGift="foundedMovies"></router-view>
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
            apiUrl: 'https://api.themoviedb.org/3/search/movie',
            searchMovies: '',

            // founded datas da passare a chi vuoi
            foundedMovies: [],
        }
    },
    methods: {
        // stai salvando il risultato passato mediante la emit nella variabile searchMovies,
        // poi con getMovies richiami questa variabile, non necessaria, essendo che potresti passare il valore della emit direttamente alla funzione getMovies()
        searchMoviesFunction(result) {
            console.log(`App.vue is saying:  ${result}`);
            this.searchMovies = result;
        },
        getMovies(wha) {
            axios.get(`${this.apiUrl}?api_key=${this.apiKey}&query=${wha}`)
                .then((result) => {
                    // console.log(result);
                    this.foundedMovies = result.data.results;
                    console.log(this.foundedMovies);
                })
                .catch((error) => {
                    console.warn(error)
                })
        }
    },
    watch: {
        // esegui tutte le volte che cambia il valore di searchMovies, richiami getMovies col newVal
        searchMovies: function (newVal, oldVal) {
            this.getMovies(newVal);
        }
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
