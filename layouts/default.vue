<template>
  <v-app :style="{ background: $vuetify.theme.themes[theme].background }">
    <app-bar />

    <div id="page-content" class="mx-xs-0 mx-xs-md-3">
      <v-main>
        <Nuxt />
      </v-main>
    </div>

    <social-bar position="right" fixed desktop-only />

    <watermark>Saxe</watermark>
  </v-app>
</template>

<script>
import Vue from 'vue';
import Watermark from '~/components/Watermark.vue';
import AppBar from '../components/AppBar.vue';

export default Vue.extend({
  name: 'DefaultLayout',
  components: { Watermark, AppBar },
  computed: {
    theme() {
      return this.$vuetify.theme.dark ? 'dark' : 'light';
    },
  },
});
</script>

<style lang="scss" scoped>
* {
  cursor: default;

  body {
    #page-content {
      z-index: 1;
      padding-top: 2em;
    }
  }

  .icon {
    height: 1.5em;
  }
}
</style>
