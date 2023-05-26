<template>
    <StandardCardComponent :item="person"/>
</template>

<script>
import StandardCardComponent from "./StandardCardComponent.vue";

export default {
    mounted() {
    },
    props: {
        person: {
            type: Object,
            required: true,
        }
    },
    components: {
        StandardCardComponent,
    },
}
</script>

<style lang="scss" scoped>
</style>
