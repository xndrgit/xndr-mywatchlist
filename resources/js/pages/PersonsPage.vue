<template>
    <div class="container-lg">
        <div class="row">
            <div class="col-12 cards-netflix">
                <PersonsListComponent v-for="person in foundedTrendingPersonsGift" v-if="!foundedPersonsGift.length > 0"
                                      :key="person.id" :person="person"/>
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
    }
}
</script>

<style lang="scss" scoped>

.row {
    min-height: 80vh;

    .cards-netflix {
        display: flex;
        flex-wrap: wrap;
    }
}

</style>
