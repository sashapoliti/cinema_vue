<template>
  <header>
    <div class="navbar navbar-expand-lg p-0" id="header-nav">
      <ul class="navbar-nav w-100 d-flex justify-content-evenly py-1 fs-1">
        <li
          class="nav-item d-flex align-items-center"
          v-for="(item, index) in menuItems"
          :key="index"
        >
          <router-link
            class="nav-link"
            :to="{ name: item.routeName }"
            active-class="active"
          >
            {{ item.name }}
          </router-link>
        </li>
      </ul>
    </div>
    <div class="admin-area">
      <a class="nav-link" href="http://localhost:8000">
        <img src="/images/engine-removebg-preview.png" alt="" />
      </a>
    </div>
  </header>
</template>

<script>
export default {
  name: "HeaderComponent",
  data() {
    return {
      menuItems: [
        {
          name: "Home",
          routeName: "home",
        },
        {
          name: "Movies",
          routeName: "movies",
        },
        {
          name: "Rooms",
          routeName: "rooms",
        },
        {
          name: "About Us",
          routeName: "about",
        },
        {
          name: "Contact",
          routeName: "contact",
        },
      ],
    };
  },
};
</script>

<style lang="scss" scoped>
@use "../assets/styles/partials/_variables.scss" as *;

header {
  position: fixed;
  top: 0;
  left: 0;
  padding: 20px;
  height: 90px;
  width: 100%;

  .admin-area {
    position: fixed;
    right: 20px;
    top: 20px;

    a {
      width: 50px;
      aspect-ratio: 1 / 1;
      transition: filter 0.3s, transform 0.3s;
      img {
        width: 100%;
        filter: brightness(0.8);
      }
      &:hover {
        filter: brightness(0.8);
        transform: scale(1.4);
      }
    }
  }

  #header-nav {
    position: relative;
    width: 60%;
    height: 100%;
    margin: 0 auto;
    background-color: $color-blue;
    clip-path: polygon(0 0, 100% 0, 98% 100%, 2% 100%);

    ul {
      background-color: #fcf6dd;
      position: absolute;
      top: 4px;
      left: 4px;
      width: calc(100% - 8px);
      height: calc(100% - 8px);
      clip-path: polygon(0.3% 0, 99% 0, 97.3% 100%, 2% 100%);
    }

    .nav-link {
      color: $color-red;
      font-size: 2.3rem;
      padding: 0;
      margin: 0;
      transition: filter 0.3s, transform 0.3s;

      a {
        line-height: 0;
      }
      &.active {
        color: $color-blue;
      }

      &:hover {
        filter: brightness(1.2);
        transform: scale(1.4);
      }
    }
  }
}
</style>
