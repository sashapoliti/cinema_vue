<template>
  <button
    type="button"
    class="btn btn-primary"
    data-bs-toggle="modal"
    :data-bs-target="`#${movie.id}Modal`"
  >
    <div class="card">
      <img :src="movie.thumb" class="card-img-top" :alt="movie.title" />
    </div>
  </button>

  <!-- Modal -->
  <div
    class="modal fade"
    :id="`${movie.id}Modal`"
    tabindex="-1"
    aria-labelledby="exampleModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog modal-dialog-centered modal-dialog-scrollable">
      <div class="modal-content">
        <div class="modal-body">
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
          <!-- movie -->
          <div class="movie-card">
            <div class="basic-info text-center px-5">
              <h2>{{ movie.title }}</h2>
              <p>
                <small
                  >Release: {{ movie.release_date }} | Language:
                  {{ movie.language }} | Minutes: {{ movie.minutes }}</small
                >
              </p>
              <p>{{ movie.description }}</p>
            </div>
            <ReviewCarousel
              class="review-carousel ms-auto"
              :reviews="movie.reviews"
            />
            <div class="projections-title text-center">
              <div
                class="title d-flex align-items-center justify-content-center"
              >
                <img
                  class="icon"
                  src="/images/projections-icon.png"
                  alt="Movie section"
                />
                <img
                  class="text"
                  src="/images/projections-title.png"
                  alt="Movie title"
                />
              </div>
              <button @click="scrollToProjections">
                <i class="fa-solid fa-angles-down"></i>
              </button>
            </div>
          </div>
          <!-- projections -->
          <div ref="projectionsList" class="projections-card">
            <ul>
              <li
                class="d-flex align-items-center"
                v-for="([date, projections], index) in sortedProjections"
                :key="index"
              >
                <div class="date">
                  <button :class="{ 'active': selectedDate === date }" @click="toggleDate(date)">
                    {{ formatDate(date) }}
                  </button>
                </div>
                <div class="date-info d-flex" :class="{ 'd-none': selectedDate !== date }">
                  <div class="d-flex align-items-center justify-content-center" v-for="projection in projections" :key="projection.id">
                    <span class="time">{{ formatTime(projection.slot.start_time) }}</span>
                    <span class="room">{{ projection.room.name }}</span>
                    <span class="isense d-flex align-items-center justify-content-center" :class="{ 'invisible': !projection.room.isense  }">i</span>
                    <span class="price">{{ projection.ticket_price }}€</span>
                  </div>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { store } from "@/store";
import ReviewCarousel from "./ReviewCarousel.vue";
import { ref, computed } from "vue";

export default {
  name: "MovieComponent",
  components: {
    ReviewCarousel,
  },
  props: {
    movie: Object,
  },
  setup() {
    const projectionsList = ref(null);

    const scrollToProjections = () => {
      if (projectionsList.value) {
        projectionsList.value.scrollIntoView({ behavior: "smooth" });
      }
    };

    return {
      projectionsList,
      scrollToProjections,
    };
  },
  data() {
    return {
      store,
      selectedDate: null,
    };
  },

  methods: {
    formatDate(dateString) {
      const date = new Date(dateString);
      const options = { day: "2-digit", month: "short" };
      return date.toLocaleDateString("en-US", options);
    },
    toggleDate(date) {
      this.selectedDate = this.selectedDate === date ? null : date;
    },
    formatTime(timeString) {
      const [hours, minutes] = timeString.split(":");
      return `${hours}:${minutes}`;
    }
  },
  computed: {
  groupedProjections() {
    return this.movie.movie_rooms.reduce((acc, projection) => {
      const date = new Date(projection.date_projection)
        .toISOString()
        .split("T")[0];
      if (!acc[date]) {
        acc[date] = [];
      }
      acc[date].push(projection);
      // Ordina le proiezioni per orario
      acc[date].sort((a, b) => {
        const timeA = a.slot.start_time;
        const timeB = b.slot.start_time;
        return timeA.localeCompare(timeB);
      });
      return acc;
    }, {});
  },
  sortedProjections() {
    return Object.entries(this.groupedProjections).sort(
      ([dateA], [dateB]) => new Date(dateA) - new Date(dateB)
    );
  }
},
  mounted() {},
};
</script>

<style lang="scss" scoped>
@use "../assets/styles/partials/_variables.scss" as *;
button {
  width: 100%;
  margin: 0;
  padding: 0;
  border: none;
  border-radius: 20px;
  .card {
    height: 400px;
    overflow: hidden;
    border-radius: 20px;
    border: 4px solid $color-yellow;
    cursor: pointer;
    transition: transform 0.3s;
    &:hover {
      transform: scale(1.1);
    }
    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      object-position: top;
    }
  }
}
.modal {
  .modal-dialog {
    width: auto;
    max-width: 800px;
    .modal-content {
      height: 800px;
      border: none;
      overflow: hidden;
      .modal-body {
        padding: 0;
        position: relative;
        background-color: $color-red;
        /* Per browser WebKit (Chrome, Safari) */
        &::-webkit-scrollbar {
          display: none; /* Nasconde la scrollbar */
        }

        /* Per Firefox */
        scrollbar-width: none; /* Nasconde la scrollbar */

        /* Soluzione cross-browser per nascondere la scrollbar ma mantenere lo scorrimento */
        &.hidden-scrollbar {
          overflow: hidden;

          &::before {
            content: "";
            display: block;
            height: 100%;
            overflow-y: scroll;
            visibility: hidden;
          }

          > * {
            overflow-y: scroll;
            margin-right: -17px; /* Regola questo valore se necessario */
            padding-right: 17px; /* Regola questo valore se necessario */
          }
        }
        button {
          position: absolute;
          top: 10px;
          right: 10px;
          width: 35px;
          height: 35px;
        }
        .movie-card {
          width: 800px;
          aspect-ratio: 1 / 1;
          background-image: url(/images/modal-bg.png);
          background-repeat: no-repeat;
          background-size: cover;
          .basic-info {
            padding-top: 150px;
            h2 {
              color: $color-white;
              font-size: 3rem;
            }
            p {
              color: $color-white;
              font-style: italic;
              &:first-of-type {
                margin: 0;
                margin-top: -15px;
              }
            }
          }
          .review-carousel {
            position: absolute;
            right: 10px;
            top: calc(50% - 95px);
          }
          .projections-title {
            position: absolute;
            bottom: 25px;
            right: calc(50% - 157px);
            .title {
              .icon {
                width: 10ch;
              }
              .text {
                width: 250px;
              }
            }
            button {
              position: static;
              background-color: transparent;
              color: $color-blue;
              font-size: 1.5rem;
              transition: color 0.3s, transform 0.3s;
              &:hover {
                color: $color-white;
                transform: scale(1.4);
              }
            }
          }
        }
        .projections-card {
          ul {
            list-style-type: none;
            padding: 0;
            margin: 0;
            margin-top: 10px;
            li {
              .date {
                button {
                  width: 80px;
                  height: 40px;
                  position: static;
                  background-color: transparent;
                  border-radius: 0;
                  background-color: $color-blue;
                  color: $color-white;
                  font-size: 1.5rem;
                  transition: color 0.3s;
                  &:hover {
                    color: $color-red;
                  }
                  &.active {
                    color: $color-red;
                  }
                }
              }
              .date-info {
                height: 40px;
                width: calc(100% - 80px);                
                div {
                  height: 100%;
                  width: calc(100% / 3);
                  .time {
                    background-color: $color-yellow;
                    padding: 0 5px;
                    margin-right: 5px;
                  }
                  .room {
                    font-size: 1.3rem;
                  }
                  .isense {
                    width: 20px;
                    height: 20px;
                    font-size: 1.3rem;
                    color: $color-yellow;
                    background-color: $color-blue;
                    border-radius: 20px;
                    margin: 0 5px 0 2px;
                  }
                  /* .price {

                  } */
                }
              }
            }
          }
        }
      }
    }
  }
}
</style>
