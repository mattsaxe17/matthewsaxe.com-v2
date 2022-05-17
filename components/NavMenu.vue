<template>
  <div id="nav-menu">
    <div id="desktop-menu" class="d-none d-md-block">
      <nav-menu-items :links="links" />
    </div>

    <div id="mobile-menu" class="d-md-none">
      <img class="icon" src="/menu.svg" alt="menu icon" @click="$emit('toggleNavDrawer')" />
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import NavMenuItems from './NavMenuItems.vue';
export default Vue.extend({
  components: {
    NavMenuItems,
  },
  props: {
    navDrawer: {
      type: Boolean,
    },
    links: {
      type: Array,
    },
  },
});
</script>

<style lang="scss" scoped>
#nav-menu {
  height: 50%;
  display: flex;
  align-items: center;
}

#mobile-menu {
  .icon {
    height: 1.5em;
  }
}
</style>