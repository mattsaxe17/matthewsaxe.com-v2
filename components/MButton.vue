<template>
  <v-btn :text="text" :href="href" :class="{ colored }">
    <slot></slot>
  </v-btn>
</template>

<script>
export default {
  name: 'MButton',
  props: {
    text: {
      type: Boolean,
      default: false,
    },
    href: {
      type: String,
      default: null,
    },
    colored: {
      type: Boolean
    }
  },
};
</script>

<style lang="scss" scoped>
a.colored {
  background-color: var(--v-secondary-base) !important;
}
</style>
