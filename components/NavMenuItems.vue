<template>
  <div>
    <nav :class="{ mobile }">
      <div class="menu-link-container">
        <div v-for="(link, ind) in links" :key="link.href" class="menu-link-wrapper">
          <nuxt-link v-if="!link.external" :to="link.href" class="menu-link">
            <span class="prefix">{{ `00${ind}`.slice(-2) }}.&nbsp;</span>
            {{ link.label }}&nbsp;
            <span class="suffix">{{ link.suffix }}</span>
          </nuxt-link>

          <a v-else :href="link.href" class="menu-link">
            <span class="prefix">{{ `00${ind}`.slice(-2) }}.&nbsp;</span>
            {{ link.label }}&nbsp;
            <span class="suffix">{{ link.suffix }}</span>
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
</template>

<script>
export default {
  props: {
    mobile: {
      type: Boolean,
      default: false,
    },
    links: {
      type: Array,
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

    .menu-link-wrapper {
      display: flex;
      align-items: center;

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

        .suffix {
          font-size: 12px;
          color: var(--v-accent-lighten3);
        }

        &:hover {
          padding-bottom: 0.25em;
          color: var(--v-accent-lighten3);
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
</style>
