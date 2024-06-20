<template>
  <div
    class="carousel-container d-flex align-items-center justify-content-between"
    v-if="reviews.length"
  >
    <button class="btn" @click="prevReview" v-if="reviews.length > 1">
      <i class="fa-solid fa-chevron-left"></i>
    </button>

    <div
      class="review-card text-center"
      :class="{ 'm-a': reviews.length === 1 }"
    >
      <div class="title d-flex align-items-center justify-content-center">
        <img class="icon" src="/images/review-icon.png" alt="Review section" />
        <img class="text" src="/images/reviews-title.png" alt="Movie title" />
      </div>
      <transition name="fade" mode="out-in">
        <div :key="currentReview">
          <p>{{ currentReview.comment }}</p>
          <p>
            <span
              v-for="(star, index) in stars"
              :key="index"
              class="fa"
              :class="star"
            ></span>
          </p>
          <p>
            <strong>- {{ currentReview.author }}</strong>
          </p>
        </div>
      </transition>
    </div>

    <button class="btn" @click="nextReview" v-if="reviews.length > 1">
      <i class="fa-solid fa-chevron-right"></i>
    </button>
  </div>
</template>

<script>
export default {
  name: "ReviewCarousel",
  props: {
    reviews: Array,
  },
  data() {
    return {
      currentIndex: 0,
      intervalId: null,
    };
  },
  methods: {
    prevReview() {
      if (this.currentIndex > 0) {
        this.currentIndex--;
      } else {
        this.currentIndex = this.reviews.length - 1;
      }
    },
    nextReview() {
      if (this.currentIndex < this.reviews.length - 1) {
        this.currentIndex++;
      } else {
        this.currentIndex = 0;
      }
    },
    startAutoAdvance() {
      this.intervalId = setInterval(this.nextReview, 7000);
    },
    stopAutoAdvance() {
      clearInterval(this.intervalId);
      this.intervalId = null;
    },
  },
  mounted() {
    this.startAutoAdvance();
  },
  beforeDestroy() {
    this.stopAutoAdvance();
  },
  computed: {
    currentReview() {
      return this.reviews[this.currentIndex];
    },
    stars() {
      const fullStars = Math.floor(this.currentReview.rating);
      const emptyStars = 5 - fullStars;
      return [
        ...Array(fullStars).fill("fa-star"),
        ...Array(emptyStars).fill("fa-star-o"),
      ];
    },
  },
};
</script>

<style lang="scss" scoped>
@use "../assets/styles/partials/_variables.scss" as *;
.carousel-container {
  width: 350px;
  height: 250px;
  .review-card {
    margin-top: -40px;
    .title {
      .icon {
        width: 50px;
      }
      .text {
        margin-top: -5px;
        width: 150px;
      }
    }
    p {
      margin: 0;
    }
    &.m-a {
      margin: 0 auto;
    }
  }
  button {
    transition: color 0.3s, transform 0.3s;
    &:hover {
      color: $color-red;
      transform: scale(1.6);
    }
  }
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
