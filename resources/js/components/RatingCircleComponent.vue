<template>
    <div class="rating-circle">
        <span class="rating-vote">{{ vote.toFixed(2) }}</span>
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
    width: 60px;
    height: 60px;
    border-radius: 50%;
    font-size: 24px;
    font-weight: bold;
    color: #fff;
    text-align: center;
    background-color: #999;
    font-family: 'Montserrat', sans-serif;
    cursor: pointer;
    transition: transform 0.2s ease-in-out, background-color 0.2s ease-in-out;
}

.rating-circle:hover {
    transform: scale(1.1);
    background-color: #666;
}

.rating-circle:active {
    transform: scale(0.9);
    background-color: #333;
}

.low {
    background-color: #f44336;
}

.mid {
    background-color: #ff9800;
}

.high {
    background-color: #4caf50;
}

.rating-text {
    display: block;
    margin-top: 5px;
    font-size: 14px;
    font-weight: normal;
}
</style>
