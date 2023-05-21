<template>
    <div class="card-netflix">
        <div class="bg-img">
            <img class="img-fluid" src="https://cdn.dribbble.com/users/354375/screenshots/3309042/cat.gif">
        </div>
        <a href="#">
            <div class="content">
                <h2>{{ movie.title }}</h2>
            </div>
        </a>
    </div>
</template>

<script>
export default {
    mounted() {
    },
    props: {
        movie: {
            type: Object,
            required: true,
        }
    }
}
</script>

<style lang="scss" scoped>

.card-netflix {
    position: relative;
    //vertical-align: middle;
    //display: inline-block;

    min-width: 200px;
    height: 120px;
    background-color: black;

    margin: 1rem 0;

    overflow: hidden;
    cursor: pointer;

    transition-duration: .5s;

    .bg-img {
        position: absolute;

        min-width: 200px;
        height: 120px;

        background-size: cover;
        background-position: center top;
    }

    &:hover {
        transition-delay: .5s;


        a {
            .content {
                transform: translateY(0) translateX(-50%);
                transition-delay: .75s;
                opacity: 1;
            }
        }
    }

    a {
        color: white;
        text-decoration: none;
        cursor: pointer;

        width: 100%;
        height: 100%;

        display: block;

        position: relative;

        z-index: 2;

        .content {
            width: 200px;

            background: linear-gradient(transparent, rgba(0, 0, 0, .75));
            width: 100%;
            height: 100px;

            position: absolute;
            bottom: 0;
            left: 50%;

            transform: translateY(100%) translateX(-50%);
            transition-duration: 1s;
            opacity: 0;
            padding: 40px 10px 10px 10px;


            h2 {
                font-weight: 300;
                color: white;
                font-size: 14px;
            }
        }
    }
}

</style>
