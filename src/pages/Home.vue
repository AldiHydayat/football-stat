<template>
  <nav-bar />
  <section id="home">
    <div class="container">
      <div class="text-content">
        <h3>Football Statistics</h3>
        <p>Standings, Matches, Teams, Competitions.</p>
      </div>
      <div class="img-content">
        <img src="@/assets/football.png" alt="chart" />
      </div>
    </div>
  </section>
</template>

<script>
import NavBar from "../components/NavBar.vue";

export default {
  name: "Home",
  components: {
    NavBar,
  },
};
</script>

<style lang="scss" scoped>
section {
  padding-top: 100px;
  min-height: 100vh;
  position: relative;
  box-sizing: border-box;

  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    @include sm {
      flex-direction: column;
    }
  }

  .text-content {
    font-family: $reem;
    width: 50%;
    z-index: 89;
    position: relative;

    @include sm {
      width: 100%;
    }

    h3 {
      font-size: 64px;
      font-weight: 500;
      @include sm {
        font-size: 36px;
        font-weight: 500;
      }
    }

    p {
      font-size: 36px;
      font-weight: 500;
      @include sm {
        font-size: 18px;
        font-weight: 500;
      }
    }
  }

  .img-content {
    img {
      position: relative;
      z-index: 10;
      width: 100%;
      max-width: 700px;
      height: auto;
    }
  }
}
</style>
