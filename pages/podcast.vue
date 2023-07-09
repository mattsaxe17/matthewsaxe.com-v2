<template>
  <div>
    <section id="episodes-wrapper" v-id="!!feed?.items?.length">
      <div v-for="episode in episodes" :key="episode.guid">
        <!-- <div class="episode">
          {{ episode.title }}
          <img :src="episode.itunes.image" />
        </div> -->
        <iframe :src="episode.link.replace('/episodes', '/embed/episodes')" class="episode" scrolling="no"></iframe>
      </div>
    </section>

    <m-footer>
      <nuxt-content :document="footer" />
    </m-footer>
  </div>
</template>

<script>
import { orderBy } from 'lodash';
import Parser from 'rss-parser';
const parser = new Parser();

export default {
  async asyncData({ $content }) {
    const footer = await $content('footer').fetch();

    return {
      footer,
    };
  },
  data: () => {
    return { feed: {} };
  },
  computed: {
    episodes() {
      return orderBy(this.feed.items, (episode) => new Date() - new Date(episode.pubDate));
    },
  },
  async created() {
    this.feed = await parser.parseURL(this.$config.rssFeedUrl);
    console.log(this.feed);
  },
};
</script>

<style lang="scss">
#episodes-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 4em;

  .episode {
    width: min(750px, 90vw);
    border: none;
    color: var(--v-accent-lighten3);

    div {
      background-color: transparent !important;
    }
  }
}

section {
  display: flex;
  justify-content: center;
  padding: 4em 0 20vw 0;

  .section-content {
    width: 90%;
    max-width: 1100px;

    .nuxt-content-container {
      max-width: 900px;
      padding: 0 2em;
      margin: auto;
    }
  }
}

h1,
h2,
h3,
h4,
h5,
h6 {
  font-family: $display-font;
}

p {
  font-family: $main-font;
  color: var(--v-accent-lighten3);
}

section#hero {
  height: 100vh;
  padding-bottom: 0;
  padding-top: 0;
  display: flex;
  align-items: center;

  .section-content {
    padding: 0;
    max-width: 100%;
    width: clamp(300px, 90vw, 1100px);
    display: flex;
    justify-content: center;

    .nuxt-content {
      max-width: 100%;
      width: clamp(300px, 90vw, 1100px);
    }

    .nuxt-content-container {
      max-width: 100%;
      width: clamp(300px, 90vw, 1100px);
    }
  }

  h1,
  h2,
  h3,
  h4,
  h5,
  h6,
  p,
  button {
    padding: 0.15em 0;
    animation: $fade-in;
    animation-timing-function: ease-out;
    line-height: 1em;
  }

  h1 {
    font-size: 1.25em;
    color: var(--v-primary-base);
    animation-delay: 0.25s;
  }

  h2 {
    animation-delay: 0.5s;
    font-size: clamp(40px, 8vw, 90px);
  }

  h3 {
    animation-delay: 0.75s;
    font-size: clamp(35px, 6.5vw, 75px);
    line-height: 0.9em;
    padding-bottom: 0.4em;
    color: var(--v-accent-lighten3);
  }

  p {
    animation-delay: 1s;
    line-height: 1.25em;
    font-size: 1em;
    padding-bottom: 2em;
    max-width: 650px;
  }

  .v-btn {
    $horizontal-padding: max(2em, 2.5vw);
    $vertical-padding: max(0.1em, 1.25vw);
    animation-delay: 1.25s;
    background-color: var(--v-secondary-base);
    padding: $vertical-padding $horizontal-padding;
    font-size: clamp(14px, 3vw, 20px);
  }
}
</style>
