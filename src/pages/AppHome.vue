<template>
    <div id="jumbo" class="d-flex align-items-center justify-content-center">
        <img src="/images/drive-in.png" alt="">
    </div>
</template>

<script>
import CardsComponent from '@/components/CardsComponent.vue';
import 'vue3-carousel/dist/carousel.css'
import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel'
import axios from "axios";
import { store } from "../store";
export default {
    name: "AppHome",
    components: {
        Carousel,
        Slide,
        Pagination,
        Navigation,
        CardsComponent
    },
    data() {
        return {
            store,
            projections: [],
            movies: []
        }
    },
    methods: {
        getWeeklyProjections() {
            axios.get(this.store.apiBaseUrl + "/movies").then((response) => {
                console.log(response.data);
                this.projections = response.data.results;
                this.store.movies = response.data.results;
                console.log(this.store.movies);
            })
        },
        getMovies() {
            axios.get(this.store.apiBaseUrl + "/movies").then((response) => {
                console.log(response.data);
                this.movies = response.data.results;
            });
        },
    },
    mounted() {
        this.getWeeklyProjections();
        this.getMovies();
    }
}
</script>

<style lang="scss" scoped>
@use '../assets/styles/partials/_variables.scss' as *;

#jumbo {
    width: 100%;
    height: 100%;
    img {
        height: 100%;
        object-fit: cover;
    }
  }
</style>