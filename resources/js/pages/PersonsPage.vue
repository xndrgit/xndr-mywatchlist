<template>
    <div class="container-lg">
        <div class="row">
            <div class="col-12 cards-netflix">
                <PersonsListComponent v-for="person in foundedPersonsGift" :key="person.id" :person="person"/>
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
