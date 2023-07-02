<template>
    <div class="container-lg">
        <div class="row">
            <div class="col-12 cards-netflix">
                <img v-if="!foundedPersonsGift.length > 0" :src="imagePath('trendingpersons.png')"
                     alt="TrendingPersonsImage"
                     class="img-fluid title-list-trending">
                <PersonsListComponent v-for="person in foundedTrendingPersonsGift" v-if="!foundedPersonsGift.length > 0"
                                      :key="person.id" :person="person"/>
                <img v-if="foundedPersonsGift.length > 0" :src="imagePath('persons.png')" alt="PersonsImage"
                     class="img-fluid title-list-trending">
                <PersonsListComponent v-for="person in foundedPersonsGift" v-if="foundedPersonsGift.length > 0"
                                      :key="person.id" :person="person"/>
            </div>
        </div>
    </div>
</template>

<script>
import PersonsListComponent from "../components/PersonsListComponent.vue";

export default {
    name: 'PersonsPage',
    mounted() {
        console.log('PersonsPage mounted.')
    },
    components: {
        PersonsListComponent,
    },
    props: {
        foundedPersonsGift: Array,
        foundedTrendingPersonsGift: Array,
    },
    methods: {
        imagePath(name) {
            return require(`../../../public/assets/${name}`);
        }
    }
}
</script>

<style lang="scss" scoped>

.row {
    min-height: 80vh;

    .title-list-trending {
        height: fit-content;
        width: fit-content;
        padding: 1rem 10rem;
    }

    .cards-netflix {
        display: flex;
        flex-wrap: wrap;
    }
}

</style>
