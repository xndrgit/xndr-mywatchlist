<template>
    <div class="wrapper col-3">
        <div class="card card--rounded wrapper__front">
            <div class="card__header">
                <!--                <img-->
                <!--                    :src="-->
                <!--                        item.poster_path-->
                <!--                            ? `https://image.tmdb.org/t/p/w220_and_h330_face/${item.poster_path}`-->
                <!--                            : item.profile_path-->
                <!--                            ? `https://image.tmdb.org/t/p/w220_and_h330_face/${item.profile_path}`-->
                <!--                            : 'https://via.placeholder.com/220x330?text=Not+Available'-->
                <!--                    "-->
                <!--                    alt="poster"-->
                <!--                    class="card__image"-->
                <!--                />-->
                <img :src="getImage(item)" alt="poster" class="card__image"/>


            </div>

            <button v-if="item.vote_average > 0"
                    class="p-0 btn btn--front btn--transparent btn--circle position-absolute ">
                <RatingCircleComponent :vote="item.vote_average"/>
            </button>


        </div>
        <div class="card card--rounded wrapper__back">
            <div class="card__header">
                <!--                <img-->
                <!--                    :src="-->
                <!--                        item.poster_path-->
                <!--                            ? `https://image.tmdb.org/t/p/w220_and_h330_face/${item.poster_path}`-->
                <!--                            : item.profile_path-->
                <!--                            ? `https://image.tmdb.org/t/p/w220_and_h330_face/${item.profile_path}`-->
                <!--                            : 'https://via.placeholder.com/220x330?text=Not+Available'-->
                <!--                    "-->
                <!--                    alt="snowpiercer banner"-->
                <!--                    class="card__image"-->
                <!--                />-->
                <img
                    :src="getImage(item)"
                    alt="snowpiercer banner"
                    class="card__image"
                />
            </div>
            <div class="card__body">
                <div class="flex justify-between items-center">
                    <div>
                        <button class="btn btn--transparent btn--circle">
                            <svg
                                class="card__icon"
                                fill="none"
                                height="24"
                                viewBox="0 0 24 24"
                                width="24"
                                xmlns="http://www.w3.org/2000/svg"
                            >
                                <path
                                    d="M21.44 10.72L5.96 2.98A1.38 1.38 0 004 4.213v15.474a1.373 1.373 0 002 1.233l15.44-7.74a1.38 1.38 0 000-2.467v.007z"
                                />
                            </svg>
                        </button>
                        <button class="btn btn--transparent btn--circle">
                            <svg
                                class="card__icon"
                                fill="none"
                                height="24"
                                viewBox="0 0 24 24"
                                width="24"
                                xmlns="http://www.w3.org/2000/svg"
                            >
                                <path
                                    d="M12 0a1.5 1.5 0 011.5 1.5v9h9a1.5 1.5 0 110 3h-9v9a1.5 1.5 0 11-3 0v-9h-9a1.5 1.5 0 110-3h9v-9A1.5 1.5 0 0112 0z"
                                />
                            </svg>
                        </button>
                        <button v-if="item.vote_average > 0" class="p-0 btn btn--transparent btn--circle">
                            <RatingCircleComponent :vote="item.vote_average"/>
                        </button>
                        <!--                        <button class="btn btn&#45;&#45;transparent btn&#45;&#45;circle">-->
                        <!--                            <svg-->
                        <!--                                class="card__icon"-->
                        <!--                                fill="currentColor"-->
                        <!--                                height="24"-->
                        <!--                                viewBox="0 0 24 24"-->
                        <!--                                width="24"-->
                        <!--                                xmlns="http://www.w3.org/2000/svg"-->
                        <!--                            >-->
                        <!--                                <path-->
                        <!--                                    d="M4.875 10.5h-3.75C.504 10.5 0 11.004 0 11.625v11.25C0 23.496.504 24 1.125 24h3.75C5.496 24 6 23.496 6 22.875v-11.25c0-.621-.504-1.125-1.125-1.125zM3 22.125a1.125 1.125 0 110-2.25 1.125 1.125 0 010 2.25zM18 3.818c0 1.988-1.217 3.104-1.56 4.432h4.768c1.566 0 2.785 1.3 2.792 2.723.004.841-.354 1.746-.911 2.306l-.005.006c.46 1.094.386 2.626-.437 3.725.407 1.213-.003 2.705-.768 3.504.202.825.106 1.527-.288 2.092C20.634 23.981 18.263 24 16.258 24h-.133c-2.264 0-4.116-.825-5.605-1.487-.748-.333-1.726-.745-2.468-.759a.563.563 0 01-.552-.562v-10.02c0-.15.06-.294.167-.4 1.857-1.835 2.655-3.777 4.177-5.302.694-.695.947-1.745 1.19-2.76.209-.868.645-2.71 1.591-2.71C15.75 0 18 .375 18 3.818z"-->
                        <!--                                />-->
                        <!--                            </svg>-->
                        <!--                        </button>-->
                        <!--                        <button class="btn btn&#45;&#45;transparent btn&#45;&#45;circle">-->
                        <!--                            <svg-->
                        <!--                                class="card__icon"-->
                        <!--                                fill="currentColor"-->
                        <!--                                height="24"-->
                        <!--                                viewBox="0 0 24 24"-->
                        <!--                                width="24"-->
                        <!--                                xmlns="http://www.w3.org/2000/svg"-->
                        <!--                            >-->
                        <!--                                <path-->
                        <!--                                    d="M21.856 10.561a4.353 4.353 0 00-.421-2.952 4.52 4.52 0 00-.813-3.14C20.578 1.848 18.943 0 15.328 0h-1.041C9.43 0 7.922 1.875 6 1.875h-.508A1.494 1.494 0 004.5 1.5h-3A1.5 1.5 0 000 3v11.25a1.5 1.5 0 001.5 1.5h3c.555 0 1.04-.302 1.299-.75h.33c.898.795 2.157 2.843 3.223 3.91.641.64.476 5.09 3.364 5.09 2.7 0 4.466-1.497 4.466-4.91 0-.862-.184-1.58-.415-2.18h1.71c2.278 0 4.023-1.95 4.023-4.012 0-.898-.233-1.64-.644-2.337zM3 13.875a1.125 1.125 0 110-2.25 1.125 1.125 0 010 2.25zm15.477.784h-4.874c0 1.773 1.329 2.596 1.329 4.432 0 1.113 0 2.659-2.216 2.659-.886-.886-.443-3.102-1.773-4.432-1.245-1.245-3.102-4.568-4.431-4.568H6V4.023c2.513 0 4.688-1.773 8.046-1.773h1.772c1.665 0 2.851.803 2.49 3.09.713.382 1.243 1.708.654 2.698 1.012.956.876 2.394.244 3.076.443 0 1.048.886 1.044 1.772-.004.887-.783 1.773-1.773 1.773z"-->
                        <!--                                />-->
                        <!--                            </svg>-->
                        <!--                        </button>-->
                    </div>
                    <button class="btn btn--transparent btn--circle">
                        <svg
                            class="card__icon"
                            fill="currentColor"
                            height="24"
                            viewBox="0 0 24 24"
                            width="24"
                            xmlns="http://www.w3.org/2000/svg"
                        >
                            <path
                                clip-rule="evenodd"
                                d="M2.469 6.969a.75.75 0 011.062 0L12 15.439l8.469-8.47a.75.75 0 111.062 1.062l-9 9a.75.75 0 01-1.062 0l-9-9a.75.75 0 010-1.062z"
                                fill-rule="evenodd"
                            />
                        </svg>
                    </button>
                </div>

                <p class="card__title text">
                    <!--                    <span class="text&#45;&#45;bold">{{ item.title ? item.title : item.name }}</span>-->
                    <span class="text&#45;&#45;bold">{{ getTitle(item) }}</span>
                </p>
                <div class="w-100">
                    <!--                    <span class="text&#45;&#45;muted text&#45;&#45;size10">-->
                    <!--                        {{-->
                    <!--                            item.release_date-->
                    <!--                                ? item.release_date-->
                    <!--                                : item.first_air_date-->
                    <!--                        }}-->
                    <!--                    </span>-->
                    <span class="text--muted text--size10">
                        {{ getDate(item) }}
                    </span>
                    <span class="text--muted">
                        {{ item.original_language }}️‍
                    </span>
                </div>

                <!--                <div class="card__progress flex justify-between items-center">-->
                <!--                    <div class="progressbar">-->
                <!--                        <div class="progressbar__status"></div>-->
                <!--                    </div>-->
                <!--                    <span class="text text&#45;&#45;bold text&#45;&#45;muted">51 of 52m</span>-->
                <!--                </div>-->
            </div>
        </div>
    </div>
</template>

<script>
import RatingCircleComponent from "./RatingCircleComponent.vue";

export default {
    mounted() {
    },
    components: {
        RatingCircleComponent,
    },
    props: {
        item: {
            type: Object,
            required: true,
        }
    },
    methods: {
        getTitle(item) {
            if (item.title) {
                return item.title;
            }
            return item.name;
        },
        getDate(item) {
            if (item.release_date) {
                return item.release_date;
            }
            return item.first_air_date;
        },
        getImage(item) {
            if (item.poster_path) {
                return `https://image.tmdb.org/t/p/w220_and_h330_face/${item.poster_path}`;
            }
            if (item.profile_path) {
                return `https://image.tmdb.org/t/p/w220_and_h330_face/${item.profile_path}`;
            }
            return 'https://via.placeholder.com/220x330?text=Not+Available';
        }
    }
}
</script>

<style lang="scss" scoped>

$clr-gray: #141414;
$clr-red: rgb(229, 9, 20);
$tablet-width: 768px;
$desktop-width: 1024px;

@mixin tablet {
    @media (min-width: #{$tablet-width}) and (max-width: #{$desktop-width - 1px}) {
        @content;
    }
}

@mixin desktop {
    @media (min-width: #{$desktop-width}) {
        @content;
    }
}

img {
    width: 100%;
    height: 100%;
}

.text {
    font-size: 0.5rem;

    @include tablet {
        font-size: 0.7rem;
    }

    @include desktop {
        font-size: 0.9rem;
    }

    &--bold {
        font-weight: 700;
        margin-right: 0.3rem;
    }


    &--muted {
        color: grey;
    }

    &--size10 {
        font-size: 10px;
    }

    &--white {
        color: white;
    }

    &--category {
        font-size: 0.7rem;
        margin-bottom: 1rem;

        @include tablet {
            font-size: 0.9rem;
        }

        @include desktop {
            font-size: 1.1rem;
        }
    }
}

.flex {
    display: flex;
}

.justify-between {
    justify-content: space-between;
}

.items-center {
    align-items: center;
}

.wrapper {
    position: relative;
    padding: 10px;

    &__front {
        position: relative;
        transition: all 250ms ease-out;
        transition-delay: 300ms;
    }

    &__back {
        position: absolute;
        opacity: 0;
        width: 150%;
        transition: all 250ms ease-out;
        transition-delay: 100ms;
        z-index: 999;

        @include desktop {
            width: 100%;
            top: 0;
        }
    }

    &:hover {
        .wrapper__front {
            opacity: 0;
        }

        .wrapper__back {
            display: inline-block;
            opacity: 1;
            width: 100%;
            transform: scale(1.1) translateY(-10%);

            @include desktop {
                width: 100%;
            }
        }
    }
}

.card {
    overflow: hidden;
    background-color: $clr-gray;
    box-shadow: 0 0 10px 1px #0a0a0a;

    &--rounded {
        border-radius: 10px;
    }

    &--vote {
        position: absolute;

    }

    &__body {
        padding: 1.25rem 0.75rem;
    }

    &__icon {
        width: 0.6rem;
        height: 0.6rem;
        fill: white;

        @include tablet {
            width: 0.8rem;
            height: 0.8rem;
        }

        @include desktop {
            width: 1rem;
            height: 1rem;
        }
    }

    &__title {
        color: white;
        margin-top: 1.25rem;

        max-width: fit-content;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
    }

    //&__progress {
    //    margin-top: 1rem;
    //    gap: 0.75rem;
    //}
}

.btn {
    padding: 0.5rem;
    display: inline-flex;
    justify-content: center;
    align-items: center;
    border: 2px solid rgba(255, 255, 255, 0.5);
    cursor: pointer;
    transition: all 250ms;

    &--front {
        margin: .3rem;
    }

    &--transparent {
        background: transparent;
    }

    &--circle {
        border-radius: 50%;
    }

    &:hover {
        background: white;

        .card__icon {
            fill: $clr-gray;
        }
    }
}

//PROGRESS BAR
//.progressbar {
//    flex: 1;
//    height: 0.15rem;
//    border-radius: 5px;
//    background: grey;
//    overflow: hidden;
//
//    &__status {
//        width: 98%;
//        height: 100%;
//        background: $clr-red;
//    }
//}

//width: 180px;
//overflow: hidden;
//white-space: nowrap;
//text-overflow: ellipsis;
</style>
