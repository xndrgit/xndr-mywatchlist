<template>
    <StandardCardComponent :movie="tv"/>
</template>

<script>
import StandardCardComponent from "./StandardCardComponent.vue";

export default {
    mounted() {
    },
    props: {
        tv: {
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
