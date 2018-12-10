<template>
  <transition
    @enter="enter"
    @after-enter="afterEnter"
    @before-leave="beforeLeave"
    @leave="leave">
    <div
      ref="container"
      :style="style"
      class="collapsible-container">
      <slot />
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    duration: {
      type: Number,
      default: 0.3,
      validator: value => value >= 0,
    },
    delay: {
      type: Number,
      default: 0,
      validator: value => value >= 0,
    },
    easing: {
      type: String,
      default: 'ease',
      validator: (value) => {
        const easings = ['linear', 'ease', 'ease-in', 'ease-out', 'ease-in-out', 'step-start', 'step-end', 'initial', 'inherit'];
        if (easings.includes(value)) return true;
        if (value.match(/^cubic-bezier\([\d.]+(,\s?[\d.]+){3}\)$/) !== null) return true;
        return value.match(/^steps\(\d+,\s?(start|end)\)$/) !== null;
      },
    },
  },
  computed: {
    style() {
      return `{
        height: 0;
        overflow: hidden;
        transition-property: height;
        transition-duration: ${this.duration}s;
        transition-delay: ${this.delay}s;
        transition-timing-function: ${this.easing};
      }`;
    },
  },
  methods: {
    enter() {
      this.$refs.container.style.height = '0';
      this.$refs.container.style.height = `${this.$refs.container.scrollHeight}px`;
    },
    afterEnter() {
      this.$refs.container.style.height = null;
    },
    beforeLeave() {
      this.$refs.container.style.height = `${this.$refs.container.scrollHeight}px`;
    },
    leave() {
      // For some reason, merely accessing scrollHeight ensures the animation works correctly
      const _ = this.$refs.container.scrollHeight; // eslint-disable-line no-unused-vars
      this.$refs.container.style.height = '0';
    },
  },
};
</script>
