<template>
  <div>
    <nav :class="{ mobile }">
      <div class="menu-link-container">
        <nuxt-link to="/#about" class="menu-link"><span class="prefix">00.&nbsp;</span>About</nuxt-link>
        <nuxt-link to="/#projects" class="menu-link"><span class="prefix">01.&nbsp;</span>Projects</nuxt-link>
        <nuxt-link to="/#contact" class="menu-link"><span class="prefix">02.&nbsp;</span>Contact</nuxt-link>
        <a href="https://nft.matthewsaxe.com" class="menu-link"><span class="prefix">03.&nbsp;</span>NFT&nbsp;<span class="postfix">(Coming Soon!)</span></a>
        <!-- <nuxt-link to="/blog">Blog</nuxt-link> (someday baby) -->
      </div>
      <v-switch v-model="$vuetify.theme.dark" inset color="#e4602f">
        <template #label>
          <v-icon v-if="$vuetify.theme.dark">mdi-weather-night</v-icon>
          <v-icon v-else>mdi-white-balance-sunny</v-icon>
        </template>
      </v-switch>
    </nav>
  </div>
</template>

<script>
export default {
  props: {
    mobile: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style lang="scss">
nav {
  display: flex;
  gap: 1em;

  .menu-link-container {
    display: flex;
    gap: 1em;
    padding-right: 2em;

    .menu-link {
      text-decoration: none;
      display: flex;
      align-items: center;

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
</style>
