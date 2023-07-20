<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-12 cards-netflix justify-content-between">
                <div class="col-12 d-flex justify-content-center">
                    <img v-if="!foundedPersonsGift.length > 0" :src="imagePath('trendingpersons.png')"
                         alt="TrendingPersonsImage"
                         class="img-fluid title-list-trending">
                </div>
                <PersonsListComponent v-for="person in foundedTrendingPersonsGift" v-if="!foundedPersonsGift.length > 0"
                                      :key="person.id" :person="person"/>
                <div class="col-12 d-flex justify-content-center">
                    <div v-if="foundedPersonsGift.length > 0" class="col-12 d-flex justify-content-center">
                    <span class="title-list-founded">
                        Founded Persons
                       <i class="fa-solid fa-check fa-bounce" style="color: #37ff00;"></i>
                    </span>

                    </div>
                    <!--                    <img v-if="foundedPersonsGift.length > 0" :src="imagePath('persons.png')" alt="PersonsImage"-->
                    <!--                         class="img-fluid title-list-trending">-->
                </div>

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
        width: 80vw;

    }

    .title-list-founded {
        color: #2eff00;
    }


    .cards-netflix {
        display: flex;
        flex-wrap: wrap;
    }
}

</style>
