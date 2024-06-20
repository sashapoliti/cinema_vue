<template>
  <div class="main-container">
    <section class="rooms">
      <div class="container">
        <div id="carouselExampleSlidesOnly" class="carousel slide pt-5" data-bs-ride="carousel">
          <div class="position-absolute " style="width: 600px; right: -450px; bottom: -280px;">
            <img src="/images/auto.png" alt="auto">
          </div>
          <div class="position-absolute " id="title" style="width: 600px; right: -300px; top: -100px; z-index: 100;">
            <img src="/images/Thank(1).png" alt="title" style=" width: 100%; height: 100%;">
          </div>
          <div class="carousel-inner position-relative" style="border-radius: 40px;">
            <div class="position-absolute w-100 h-100 z-1 "><img src="/images/rooms-border.png" alt="border"
                style=" width: 100%; height: 100%; object-fit: fill"></div>
            <div class="carousel-item active">
              <img src="/images/Kubrik.jpg" class="d-block w-100" style="width: 400px; height: 600px;" alt="Kubrik">
              <div class="carousel-caption text-start mb-3 " style="">
                <h1>{{ store.rooms[0].name }}</h1>
                <p><strong>Capacity : </strong>{{ store.rooms[0].seats }} </p>
              </div>
            </div>
            <div class="carousel-item">
              <img src="/images/Spilberg.jpg" class="d-block w-100" style="width: 400px; height: 600px;"
                alt="Hitchcock">
              <div class="carousel-caption text-start mb-3 " style="">
                <h1>{{ store.rooms[1].name }}</h1>
                <p><strong>Capacity : </strong>{{ store.rooms[1].seats }} </p>
              </div>
            </div>
            <div class="carousel-item">
              <img src="/images/Hitchcock.jpg" class="d-block w-100" style="width: 400px; height: 600px;"
                alt="Miyazaki">
              <div class="carousel-caption text-start mb-3 " style="">
                <h1>{{ store.rooms[2].name }}</h1>
                <p><strong>Capacity : </strong>{{ store.rooms[2].seats }} </p>
              </div>
            </div>
            <div class="carousel-item">
              <img src="/images/Miyazaki.jpg" class="d-block w-100" style="width: 400px; height: 600px;" alt="Spilberg">
              <div class="carousel-caption text-start mb-3 " style="">
                <h1>{{ store.rooms[3].name }}</h1>
                <p><strong>Capacity : </strong>{{ store.rooms[3].seats }} </p>
              </div>
            </div>
          </div>
          <div class="carousel-indicators mt-3">
            <button type="button" data-bs-target="#carouselExampleSlidesOnly" data-bs-slide-to="0" class="active">
              <img src="/images/Kubrik.jpg" alt="Kubrik">
            </button>
            <button type="button" data-bs-target="#carouselExampleSlidesOnly" data-bs-slide-to="1">
              <img src="/images/Spilberg.jpg" alt="Hitchcock">
            </button>
            <button type="button" data-bs-target="#carouselExampleSlidesOnly" data-bs-slide-to="2">
              <img src="/images/Hitchcock.jpg" alt="Miyazaki">
            </button>
            <button type="button" data-bs-target="#carouselExampleSlidesOnly" data-bs-slide-to="3">
              <img src="/images/Miyazaki.jpg" alt="Spilberg">
            </button>
          </div>
        </div>
      </div>
    </section>
  </div>

</template>

<script>
import axios from "axios";
import { store } from "../store";

export default {
  name: "Rooms",

  data() {
    return {
      store,
      rooms: [],
      projections: [],
    };
  },
  methods: {
    getRooms() {
      axios.get(this.store.apiBaseUrl + "/rooms").then((response) => {
        console.log(response.data);
        this.rooms = response.data.results;
      });
    },

    getProjections() {
      axios.get(this.store.apiBaseUrl + "/projections").then((response) => {
        console.log(response.data);
        this.projections = response.data.results;

      });
    },
    mounted() {
      this.getRooms();
      this.getProjections();
      console.log(this.projections);
    },
  },
};
</script>

<style lang="scss" scoped>
.rooms {
  margin-top: 100px;
}
h1 {
  font-size: 4rem;
  margin-bottom: 10px;
}

p {
  font-size: 2rem;
  margin: 0;
}

.margin {
  margin-top: 300px;
}

.title {
  margin-bottom: 20px;

  .icon {
    width: 70px;
  }

  .text {
    width: 200px;
  }
}

.carousel-indicators {
  img {
    width: 200px;
    display: block;
    border: 4px solid #da654b;
  }

  button {
    width: max-content !important;
    margin: 0 30px !important;
  }
}
</style>