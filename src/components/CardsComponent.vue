<template>
    <section class="features-icons text-center" id="rooms-section">
        <video src="/videos/video_2.mp4" autoplay loop muted class="w-100"></video>
        <div class="container">
            <h2 class="text-center pt-4 fs-1">Le nostre sale</h2>
            <div class="row">
                <div class="col-lg-3 pt-4" v-for="room in rooms" :key="room.id">
                    <div class="features-icons-item mx-auto mb-5 mb-lg-0 mb-lg-3">
                        <div class="features-icons-icon d-flex align-items-center justify-content-center">
                            <img :src="room.img_room" :alt="room.name" style="width: 150px; height: 200px">
                        </div>
                        <div class="features-icons-content">
                            <h3 class="pt-2">{{ room.name }}</h3>
                            <div><strong>Colore:</strong> {{ room.alias }}</div>
                            <div><strong>Capienza:</strong> {{ room.seats }}</div>
                            <div><strong>Prezzo base bilietto:</strong>{{ room.base_price }}$</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
import axios from "axios";
import { store } from "../store";
export default {
    name: "CardsComponent",
    data() {
        return {
            store,
            rooms: [],
        }
    },
    methods: {
        getRooms() {
            axios.get(this.store.apiBaseUrl + "/rooms").then((response) => {
                console.log(response.data);
                this.rooms = response.data.results;
            })
        }
    },
    mounted() {
        this.getRooms();
    }
}
</script>

<style lang="scss" scoped>
@use '../assets/styles/partials/_variables.scss' as *;

#rooms-section {
    height: 500px;
    width: 100%;
    position: relative;

    video {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        object-fit: cover;
        object-position: center;
        z-index: -1;
        opacity: 70%;
    }

    h2 {
        color: $color-red;
    }

    .features-icons-item {
        transition: 0.5s ease-in-out;

        &:hover {
            transform: scale(1.1);
            cursor: pointer;
        }
    }

    .features-icons-content {
        color: $color-white;
    }
}
</style>