<template>
    <div :class="{'high': vote >= 7, 'mid' : vote > 3 && vote < 7, 'low' : vote < 3 && vote > 0} "
         class="rating-circle">
        <span v-if="vote > 0" class="rating-vote">{{ vote.toFixed(2) }}</span>
        <span v-else class="rating-vote">?</span>
    </div>
</template>

<script>

export default {
    mounted() {
    },
    props: {
        vote: {
            type: Number,
            required: true,
        }
    },
    methods: {}
}
</script>

<style lang="scss" scoped>
.rating-circle {
    display: flex;
    justify-content: center;
    align-items: center;

    width: 40px;
    height: 40px;

    border-radius: 50%;

    text-align: center;
    background-color: #999;

    font-family: 'Rubik Puddles', cursive;


    transition: transform 0.2s ease-in-out, background-color 0.2s ease-in-out;
}

.low {
    background-color: #D3212C;
}

.mid {
    background-color: #FF980E;
}

.high {
    background-color: #069C56;
}

.rating-vote {
    display: block;
    font-size: 12px;
    font-weight: bold;
    color: black;
    text-shadow: 10px 10px 10px rgba(0, 0, 0, 0.5);
}
</style>
