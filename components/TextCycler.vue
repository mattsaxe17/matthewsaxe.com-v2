<template>
  <div id="outer">
    <div id="inner" ref="inner">{{ options[currentInd] }}</div>
  </div>
</template>

<script>
export default {
  props: {
    options: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      currentInterval: null,
      currentInd: 0,
    };
  },
  mounted() {
    this.currentInterval = setInterval(() => {
      this.currentInd = this.currentInd === this.options.length - 1 ? 0 : this.currentInd + 1;
      this.$refs.inner.classList.remove('active');
      this.$refs.inner.classList.add('active');
    }, 3000);
  },
  beforeDestroy() {
    this.currentInterval = null;
  },
};
</script>

<style lang="scss" scoped>
#outer {
  display: inline;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  z-index: 0;

  #inner {
    display: inline-block;
    position: relative;
    z-index: 1;

    &.active {
      animation: rotateDownAnimation ease-in-out 3000ms infinite;
    }
  }
}

@keyframes rotateDownAnimation {
  0% {
    -webkit-transform: translateZ(-1em) rotateX(90deg);
    transform: translateZ(-1em) rotateX(90deg);
  }
  10% {
    -webkit-transform: rotateX(0deg);
    transform: rotateX(0deg);
    padding-right: 0;
  }
  90% {
    -webkit-transform: rotateX(0deg);
    transform: rotateX(0deg);
    padding-right: 0;
  }
  100% {
    -webkit-transform: translateZ(-1em) rotateX(-90deg);
    transform: translateZ(-1em) rotateX(-90deg);
  }
}
</style>
