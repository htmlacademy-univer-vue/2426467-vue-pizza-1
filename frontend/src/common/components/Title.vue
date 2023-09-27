<template>
  <component :is="VARIANTS[variant].tag" :class="`title title--${variant}`"><slot /></component>
</template>

<script setup>
defineProps({
  variant: {
    type: String,
    default: "small",
    validator: value => Object.keys(VARIANTS).includes(value),
  },
});
</script>

<script>
const VARIANTS = {
  small: { tag: 'h2' },
  big: { tag: 'h1' },
};
</script>

<style lang="scss" scoped>
@import "@/assets/scss/app.scss";

.title {
  box-sizing: border-box;
  width: 100%;
  margin: 0;
  color: $black;

  &--big {
    @include b-s36-h42;
  }

  &--small {
    @include b-s18-h21;
  }
}
</style>
