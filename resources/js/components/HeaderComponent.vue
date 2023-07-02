<template>
    <header class="row">
        <nav class="col-12 navbar navbar-expand-lg navbar-dark">
            <router-link class="col-3 navbar-brand d-flex align-items-center justify-content-around" to="/">
                <img :src="imagePath('favicon.png')"
                     alt="Logo" class="img-fluid">
                <!--                     height="30" :src="srcLogo">-->
                <h2 class="font-weight-bold mb-0">MyWatchList</h2>
            </router-link>
            <!--                <ul class="navbar-nav col-2">-->
            <!--                    <li class="nav-item">-->
            <!--                        <router-link class="nav-link" to="/movies">мσνιєѕ</router-link>-->
            <!--                    </li>-->
            <!--                    <li class="nav-item">-->
            <!--                        <router-link class="nav-link" to="/series">ѕєяιєѕ</router-link>-->
            <!--                    </li>-->
            <!--                    <li class="nav-item">-->
            <!--                        <router-link class="nav-link" to="/persons">ρєяѕσиѕ</router-link>-->
            <!--                    </li>-->
            <!--                </ul>-->


            <select class="select" onchange="window.location.href=this.value;">
                <option disabled selected>🔎| Select</option>
                <option value="/movies">🎥| Movies</option>
                <option value="/series">🎬| Series</option>
                <option value="/persons">👤| Persons</option>
            </select>


            <form class="form-inline ml-auto col-6">
                <input v-model="searchAll" aria-label="Search" class="form-control mr-sm-1" placeholder="Search"
                       type="search">
                <button class="btn btn-danger my-2 my-sm-0" type="submit"
                        @click.prevent="$emit('searchAll', searchAll)">Search
                </button>
            </form>

            <div class="select col-2">
                <select id="format" v-model="selectedOption" name="format">
                    <option disabled selected>my hystory</option>
                    <option v-for="log in searchAllOldGift.slice().reverse()" :value="log">{{ log }}</option>
                </select>
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
            return require(`../../../public/assets/${filename}`);
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


    .select {
        -webkit-appearance: none;
        -moz-appearance: none;
        -ms-appearance: none;
        appearance: none;

        outline: 0;
        box-shadow: none;


        border-radius: 5px;
        padding: 2px 6px;

        text-align: start;

        background: black;
        color: white;

        &:hover {

        }
    }

}
</style>
