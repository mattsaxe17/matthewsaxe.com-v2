<template>
  <div>
    <div id="app-bar" ref="appBar">
      <nuxt-link to="/" class="menu-link logo">
        <img src="/logo.svg" alt="logo" @click="scrollToTop" />
      </nuxt-link>

      <v-spacer />

      <nav-menu :nav-drawer="navDrawer" @toggleNavDrawer="toggleNavDrawer" :links="links" />
    </div>

    <v-navigation-drawer v-model="navDrawer" class="d-md-none" right fixed :width="300">
      <div id="mobile-menu-drawer-content">
        <img class="icon" src="/x.svg" @click="toggleNavDrawer" />
        <nav-menu-items :links="links" mobile />
      </div>
      <social-bar position="right" />
    </v-navigation-drawer>
  </div>
</template>

<script>
export default {
  name: 'AppBar',
  props: {
    links: {
      type: Array,
    },
  },
  data() {
    return {
      scrollPos: 0,
      navDrawer: null,
    };
  },
  computed: {
    theme() {
      return this.$vuetify.theme.dark ? 'dark' : 'light';
    },
  },
  mounted() {
    window.onscroll = () => {
      const currentScrollPos = window.pageYOffset;
      const appBar = this.$refs.appBar;

      appBar.style.top = this.scrollPos > currentScrollPos || currentScrollPos < 30 ? '0' : '-100%';
      appBar.style.boxShadow = currentScrollPos < 30 ? 'none' : '0 10px 30px -10px black';
      appBar.style.paddingTop = currentScrollPos < 30 ? '2em' : '1.5em';
      appBar.style.paddingBottom = currentScrollPos < 30 ? '2em' : '1.5em';
      appBar.style.height = currentScrollPos < 30 ? '8em' : '6em';

      this.scrollPos = currentScrollPos;
    };
  },
  methods: {
    toggleNavDrawer() {
      this.navDrawer = !this.navDrawer;
    },
    scrollToTop() {
      window.scrollTo({ top: 0, behavior: 'smooth' });
    },
  },
};
</script>

<style lang="scss" scoped>
#mobile-menu-drawer-content {
  padding: 2em;
  z-index: 12;
  height: 100%;

  .icon {
    position: fixed;
    top: 2em;
    right: 2em;
    height: 1.5em;
  }
}

#app-bar {
  animation: $fade-in;
  animation-delay: -0.1s;
  transition-property: box-shadow, padding, height, top;
  transition-duration: 0.5s;
  opacity: 1 !important;
  background-color: var(--v-background-base);
  z-index: 2;
  width: 100vw;
  display: flex;
  align-items: center;
  position: fixed;
  height: 8em;
  padding: 2em;

  .logo {
    height: 100%;

    img {
      height: 100%;
      cursor: pointer;
    }
  }
}
</style>
