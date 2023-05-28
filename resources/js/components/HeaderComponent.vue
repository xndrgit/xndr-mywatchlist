<template>
    <header class="row">
        <nav class="col-12 navbar navbar-expand-lg navbar-dark bg-dark">
            <router-link class="navbar-brand" to="/">
                <img alt="Rick & Morty Logo"
                     height="30" :src="srcLogo">
            </router-link>
            <button aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation"
                    class="navbar-toggler"
                    data-target="#navbarNav" data-toggle="collapse" type="button">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div id="navbarNav" class="collapse navbar-collapse">
                <ul class="navbar-nav">
                    <li class="nav-item">
                        <router-link class="nav-link" to="/movies">ᴍᴏᴠɪᴇꜱ</router-link>
                    </li>
                    <li class="nav-item">
                        <router-link class="nav-link" to="/series">ꜱᴇʀɪᴇꜱ</router-link>
                    </li>
                    <li class="nav-item">
                        <router-link class="nav-link" to="/persons">ᴘᴇʀꜱᴏɴꜱ</router-link>
                    </li>
                </ul>
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
    data: function (){
        return {
            srcLogo: 'https://upload.wikimedia.org/wikipedia/commons/7/7a/Logonetflix.png',
            searchAll: '',
        }
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
}
</style>
