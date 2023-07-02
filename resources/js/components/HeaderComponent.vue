<template>
    <header class="row">
        <nav class="col-12 navbar navbar-expand-lg navbar-dark">
            <router-link class=" navbar-brand d-flex align-items-center justify-content-around" to="/">
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


            <select onchange="window.location.href=this.value;">
                <option disabled selected>🔎 Select</option>
                <option value="/">🪄 All</option>
                <option value="/movies">🎥 Movies</option>
                <option value="/series">🎬 Series</option>
                <option value="/persons">👤 Persons</option>
            </select>


            <form class="form-inline col-4">
                <input v-model="searchAll" aria-label="Search" class="form-control col-12" placeholder="Search"
                       type="search">
                <button class="btn" type="submit"
                        @click.prevent="$emit('searchAll', searchAll)">
                    <i class="fa-brands fa-searchengin fa-shake"></i>
                </button>
            </form>


            <div class="position-relative">
                <select id="format" v-model="selectedOption" class="history position-relative" name="format">
                    <option disabled selected>📜 Hystory</option>
                    <option v-for="log in searchAllOldGift.slice().reverse()" :value="log">📌 {{ log }}</option>
                </select>
                <span class="fix-selected position-absolute">{{ selectedOption == null ? "📜 History" : "" }}</span>
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


    select {
        -webkit-appearance: none;
        -moz-appearance: none;
        -ms-appearance: none;
        appearance: none;
        outline: 0;
        border: 0;


        border-radius: 25px;
        padding: 6px 10px;


        text-align: start;

        background: rgba(39, 39, 39, 0.60);
        color: white;

        transition: 0.5s;

        &:hover {
            background: rgba(39, 39, 39, 1);
        }
    }

    .fix-selected {
        top: 6px;
        left: 18px;
        pointer-events: none;
    }


    form {
        input {
            position: relative;

            border-radius: 25px;
            padding: 6px 10px;

            background: rgba(39, 39, 39, 1);

            border: 2px solid black;

            &:focus {
                background: rgba(39, 39, 39, 0.60);
                color: white;
            }
        }

        button {
            position: absolute;
            right: 16px;
            font-size: 1rem;

            background: rgba(39, 39, 39, 0.60);
            border-radius: 117px;
            padding: 3px 11px;
            border-left: 8px;
            color: white;

            &:hover {
                color: white;
            }
        }
    }

}
</style>
