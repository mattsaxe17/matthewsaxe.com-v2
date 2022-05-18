<template>
  <div id="page-wrapper">
    <div class="container">
      <div id="blog-header">
        <h1>Home</h1>

        <p>Blog stuff</p>
      </div>

      <div id="card-wrapper">
        <v-card>card 1</v-card>
        <v-card>card 2</v-card>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  layout: 'blog',
};
</script>

<style lang="scss" scoped>
#blog-header {
  margin-bottom: 3em;

  h1 {
    margin-bottom: 1em;
  }
}

.container {
  width: clamp(200px, 95vw, 1200px);
  margin: auto;
  display: flex;
  flex-direction: column;

  #card-wrapper {
    width: 100%;
    display: flex;
    gap: 3em;

    .v-card {
      padding: 2em;

      &:nth-of-type(1) {
        width: 70%;
      }

      &:nth-of-type(2) {
        width: 30%;
      }
    }
  }
}
</style>
