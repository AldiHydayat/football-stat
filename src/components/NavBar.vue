<template>
  <nav>
    <div class="container">
      <ul :class="[toggle ? 'sidebar-active' : '']">
        <li><a href="#">Home</a></li>
        <li><a href="#standings">Standings</a></li>
        <li><a href="#">Link</a></li>
        <li><a href="#">Link</a></li>
        <li><a href="#">Link</a></li>
      </ul>
      <div
        :class="[toggle ? 'toggle-active' : '', 'toggle']"
        @click="toggleClass"
      >
        <span></span>
        <div class="close">
          <span></span>
          <span></span>
        </div>
        <span></span>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "NavBar",
  data() {
    return {
      toggle: false,
    };
  },
  methods: {
    toggleClass() {
      this.toggle = !this.toggle;
    },
  },
};
</script>

<style lang="scss" scoped>
nav {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 75px;
  background-color: #1cc5dc;
  position: fixed;
  top: 0;
  z-index: 99;

  .container {
    @include sm {
      display: flex;
      justify-content: right;
    }
  }

  .toggle {
    @include sm {
      display: block;
    }
    transition: 0.5s all;

    display: none;
    span {
      width: 25px;
      height: 5px;
      background-color: white;
      display: block;
      border-radius: 50px;
      margin: 3px;
      transition: 0.5s all;
    }
  }

  .close {
    position: relative;
    span:nth-child(2) {
      position: absolute;
      top: 0;
      margin: 0 3px;
    }
  }

  .toggle-active {
    transition: 0.5s all;
    .close {
      span:nth-child(1) {
        transform: rotate(45deg);
        opacity: 100;
        transition: 0.5s all;
      }
      span:nth-child(2) {
        transform: rotate(-45deg);
        opacity: 100;
      }
    }
    span {
      opacity: 0;
      transition: 0.5s all;
    }
  }

  .sidebar-active {
    transform: translateY(0%);
    transition: 0.5s all;
  }

  ul {
    display: flex;
    justify-content: space-between;
    align-items: center;
    list-style-type: none;
    transition: 0.5s all;

    @include sm {
      position: absolute;
      top: 0;
      left: 0;
      height: 100vh;
      width: 80%;
      background-color: #1cc5dc;
      flex-direction: column;
      justify-content: space-around;
      transform: translateX(-100%);
    }

    a {
      font-family: $prompt;
      font-weight: bold;
      font-size: 24px;
      text-decoration: none;
      color: white;
    }
  }
}
</style>
