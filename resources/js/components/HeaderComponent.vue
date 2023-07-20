<template>
    <header class="row">
        <nav class="col-12 justify-content-between navbar navbar-expand-lg navbar-dark">

            <div class="col-4 d-flex align-items-center">
                <select class="selectUrl" onchange="window.location.href=this.value;">
                    <option disabled selected>🔎</option>
                    <option value="/">🪄 All</option>
                    <option value="/movies">🎥 Movies</option>
                    <option value="/series">🎬 Series</option>
                    <option value="/persons">👤 Persons</option>
                </select>

                <router-link class=" navbar-brand d-flex align-items-center justify-content-around" to="/">
                    <img :src="imagePath('favicon.png')"
                         alt="Logo" class="img-fluid logoImg">
                    <!--                     height="30" :src="srcLogo">-->
                    <h1 class="font-weight-bold mb-0 logoTitle">MyWatchList</h1>
                </router-link>
            </div>

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


            <form class="form-inline col-2">
                <input v-model="searchAll" aria-label="Search" class="form-control col-12" placeholder="Search"
                       type="search">
                <button class="btn" type="submit"
                        @click.prevent="$emit('searchAll', searchAll)">
                    <i class="fa-brands fa-searchengin fa-shake"></i>
                </button>
            </form>

            <div class="col-6 d-flex justify-content-end">
                <div class="position-relative">
                    <select id="format" v-model="selectedOption" class="history position-relative" name="format">
                        <option disabled selected>📜 Hystory</option>
                        <option v-for="log in searchAllOldGift.slice().reverse()" :value="log">📌 {{ log }}</option>
                    </select>
                    <span class="fix-selected position-absolute">{{ selectedOption == null ? "📜 History" : "" }}</span>
                </div>
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

    height: 15vh;
    background: #0f0f0f;

    display: flex;
    align-content: center;
    justify-content: space-between;

    opacity: 0.8;

    .navbar-brand {
        transition: 1s;

        .logoImg {
            height: 100px;
            margin-left: 30px;
        }

        .logoTitle {
            font-size: 3rem;
        }
    }


    select {
        -webkit-appearance: none;
        -moz-appearance: none;
        -ms-appearance: none;
        appearance: none;
        outline: 0;
        border: 0;


        border-radius: 25px;
        padding: 8px 10px;


        text-align: start;

        background: black;
        color: white;
        cursor: pointer;

        transition: 0.5s;

        &:hover {
            background: rgba(39, 39, 39, 1);
        }
    }

    .selectUrl {
        width: 50px;
        height: 50px;

        font-size: 1.3rem;
        border-radius: 50%;
    }

    .fix-selected {
        top: 8px;
        left: 14px;
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
