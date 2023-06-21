<template>
    <header class="row">
        <nav class="col-12 navbar navbar-expand-lg navbar-dark">
            <router-link class="navbar-brand col-lg-3 d-flex justify-content-center" to="/">
                <img :src="imagePath('favicon.png')"
                     alt="Logo" class="img-fluid mr-2">
                <!--                     height="30" :src="srcLogo">-->
                <h2 class="font-weight-bold">MyWatchList</h2>
            </router-link>
            <button aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation"
                    class="navbar-toggler"
                    data-target="#navbarNav" data-toggle="collapse" type="button">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div id="navbarNav" class="collapse navbar-collapse">
                <ul class="navbar-nav col-lg-4">
                    <li class="nav-item">
                        <router-link class="nav-link" to="/movies">мσνιєѕ</router-link>
                    </li>
                    <li class="nav-item">
                        <router-link class="nav-link" to="/series">ѕєяιєѕ</router-link>
                    </li>
                    <li class="nav-item">
                        <router-link class="nav-link" to="/persons">ρєяѕσиѕ</router-link>
                    </li>
                </ul>

                <div class="select col-lg-3">
                    <select id="format" v-model="selectedOption" name="format">
                        <option disabled selected>my hystory</option>
                        <option v-for="log in searchAllOldGift.slice().reverse()" :value="log">{{ log }}</option>
                    </select>
                </div>
                <form class="form-inline ml-auto">
                    <input v-model="searchAll" aria-label="Search" class="form-control mr-sm-1" placeholder="Search"
                           type="search">
                    <button class="btn btn-danger my-2 my-sm-0" type="submit"
                            @click.prevent="$emit('searchAll', searchAll)">Search
                    </button>
                </form>
            </div>
        </nav>
    </header>

</template>

<script>

import axios from "axios";

export default {
    props: {
        searchAllOldGift: Array,
    },
    data: function () {
        return {
            // https://developers.themoviedb.org/3/search/search-movies
            apiKey: 'da54add692c53fb6bacfc3b15da91484',
            apiUrlMovie: 'https://api.themoviedb.org/3/search/movie',
            apiUrlTv: 'https://api.themoviedb.org/3/search/tv',
            apiUrlPerson: 'https://api.themoviedb.org/3/search/person',


            // srcLogo: 'https://upload.wikimedia.org/wikipedia/commons/7/7a/Logonetflix.png',
            searchAll: '',
            selectedOption: null,


            // founded datas da passare a chi vuoi
            foundedMovies: [],
            foundedSeries: [],
            foundedPersons: [],


        }
    },
    methods: {
        imagePath(filename) {
            return require(`../../../public/images/${filename}`);
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
    mounted() {
        console.log('HeaderComponent mounted.')
    },
    watch: {
        // esegui tutte le volte che cambia il valore di searchMovies, richiami getMovies col newVal
        selectedOption: function (newVal, oldVal) {
            console.log(newVal);
            this.$emit('searchAll', this.selectedOption);
        }
    },
}
</script>


<style lang="scss" scoped>
header {

    height: 10vh;

    display: flex;
    align-content: center;
    justify-content: space-between;


    img {
        max-height: 30px;
    }


    select {
        -webkit-appearance: none;
        -moz-appearance: none;
        -ms-appearance: none;
        appearance: none;

        outline: 0;
        box-shadow: none;
        border: 0 !important;
        background: #5c6664;


        flex: 1;
        padding: 0 .5em;

        color: #fff;
        cursor: pointer;
        font-size: 1em;
        font-family: 'Open Sans', sans-serif;
    }

    select::-ms-expand {
        display: none;
    }

    .select {
        position: relative;
        display: flex;
        width: 10em;
        height: 3em;
        line-height: 3;
        background: #5c6664;
        overflow: hidden;
        border-radius: .25em;
    }

    .select::after {
        content: '\25BC';
        position: absolute;
        top: 0;
        right: 0;
        padding: 0 1em;
        background: #2b2e2e;
        cursor: pointer;
        pointer-events: none;
        transition: .25s all ease;
    }

    .select:hover::after {
        color: #23b499;
    }
}
</style>
