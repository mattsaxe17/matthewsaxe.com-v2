<template>
  <div id="nav-bar">
    <div id="desktop-menu" class="d-none d-md-block">
      <nav>
        <div class="menu-link-container">
          <div v-for="(link, ind) in links" :key="link.href" class="menu-link-wrapper">
            <nuxt-link v-if="!link.external" :to="link.href" class="menu-link">
              <span class="prefix">{{ `00${ind}`.slice(-2) }}.&nbsp;</span>
              {{ link.label }}&nbsp;
              <span class="postfix">{{ link.postfix }}</span>
            </nuxt-link>

            <a v-else :href="link.href" class="menu-link">
              <span class="prefix">{{ `00${ind}`.slice(-2) }}.&nbsp;</span>
              {{ link.label }}&nbsp;
              <span class="postfix">{{ link.postfix }}</span>
            </a>
          </div>
        </div>
        <v-switch v-model="$vuetify.theme.dark" inset color="#e4602f">
          <template #label>
            <v-icon v-if="$vuetify.theme.dark">mdi-weather-night</v-icon>
            <v-icon v-else>mdi-white-balance-sunny</v-icon>
          </template>
        </v-switch>
      </nav>
    </div>

    <div id="mobile-menu" class="d-md-none">
      <img src="/menu.svg" alt="menu icon" @click="$emit('toggleNavDrawer')" />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    navDrawer: {
      type: Boolean,
    },
    links: {
      type: Array,
    },
  },
};
</script>

<style lang="scss" scoped>
#nav-bar {
  height: 50%;
  display: flex;
  align-items: center;

  nav {
    display: flex;
    gap: 1em;

    .menu-link-container {
      display: flex;
      gap: 1em;
      padding-right: 2em;

      .menu-link-wrapper {
        display: flex;
        align-items: center;

        .menu-link {
          text-decoration: none;
          display: flex;
          align-items: center;
          transition: padding 0.1s ease-in-out;

          .prefix {
            font-weight: bold;
            color: var(--v-primary-base);

            &::after {
              content: ' ';
            }
          }

          .postfix {
            font-size: 12px;
            color: var(--v-accent-lighten3);
          }

          &:hover {
            color: var(--v-accent-lighten3);
            padding-bottom: 0.25em;
          }
        }
      }
    }

    &.mobile {
      display: flex;
      flex-direction: column;

      .menu-link-container {
        flex-direction: column;

        .menu-link {
          display: flex;
          flex-direction: column;
          align-items: flex-start;
        }
      }
    }
  }

  #mobile-menu {
    height: 100%;

    img {
      height: 1.5em;
    }
  }
}
</style>
