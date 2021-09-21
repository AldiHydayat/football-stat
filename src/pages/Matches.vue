<template>
  <section id="matches">
    <div class="container">
      <h3>Matches</h3>
    </div>
  </section>
</template>

<script>
export default {
  name: "Matches",
};
</script>

<style lang="scss" scoped>
section {
  padding-top: 100px;
  min-height: 100vh;
  box-sizing: border-box;

  h3 {
    font-family: $prompt;
    text-align: center;
    border-bottom: 3px solid #1cc5dc;
  }
}
</style>
