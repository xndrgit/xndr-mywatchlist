<template>
    <header class="row">
        <nav class="col-12 navbar navbar-expand-lg navbar-dark bg-dark">
            <router-link class="navbar-brand col-lg-3" to="/">
                <img alt="Rick & Morty Logo"
                     :src="imagePath('mylist.png')" class="img-fluid">
                <!--                     height="30" :src="srcLogo">-->
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
                    <select id="format" name="format">
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
export default {
    props: {
        searchAllOldGift: Array,
    },
    data: function () {
        return {
            // srcLogo: 'https://upload.wikimedia.org/wikipedia/commons/7/7a/Logonetflix.png',
            searchAll: '',
        }
    },
    methods: {
        imagePath(filename) {
            return require(`../../../public/images/${filename}`);
        },
    },
    mounted() {
        console.log('HeaderComponent mounted.')
    }
}
</script>


<style lang="scss" scoped>
header {
    height: 10vh;

    display: flex;
    align-content: center;
    justify-content: space-between;


    select {
        -webkit-appearance: none;
        -moz-appearance: none;
        -ms-appearance: none;
        appearance: none;

        outline: 0;
        box-shadow: none;
        border: 0 !important;
        background: #5c6664;
        background-image: none;

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
