<template>
  <home />
  <standings />
  <Footer />
</template>

<script>
import Home from "./pages/Home.vue";
import Standings from "./pages/Standings.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "App",
  components: {
    Home,
    Standings,
    Footer,
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
}

body {
  overflow-x: hidden;
}

@media (max-width: 599px) {
  .container {
    width: 90%;
    margin: auto;
  }
}

@media (min-width: 600px) {
  .container {
    width: 540px;
    margin: auto;
  }
}

@media (min-width: 768px) {
  .container {
    width: 720px;
    margin: auto;
  }
}

@media (min-width: 992px) {
  .container {
    width: 960px;
    margin: auto;
  }
}

@media (min-width: 1200px) {
  .container {
    width: 1140px;
    margin: auto;
  }
}

@media (min-width: 1400px) {
  .container {
    width: 1320px;
    margin: auto;
  }
}
</style>
