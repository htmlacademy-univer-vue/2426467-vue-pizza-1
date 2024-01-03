<template>
  <app-layout>
    <home-view />
  </app-layout>
</template>

<script setup>
import { HomeView } from "@/views";
import { AppLayout } from "@/layouts";
</script>

<style lang="scss">
@import "@/assets/scss/ds-system/ds.scss";

body {
  display: flex;
  flex-direction: column;
  min-width: 960px;
  min-height: 100vh;
  margin: 0;
  color: $black;
  background-color: $white;
  font-family: "Roboto", Arial, sans-serif;
  font-size: 14px;
  line-height: 16px;
  text-rendering: optimizeLegibility;
}

a {
  text-decoration: none;
}

img {
  max-width: 100%;
  height: auto;
}
</style>

<style lang="scss">
@import "@/assets/scss/ds-system/ds.scss";

body {
  display: flex;
  flex-direction: column;
  min-width: 960px;
  min-height: 100vh;
  margin: 0;
  color: $black;
  background-color: $white;
  font-family: "Roboto", Arial, sans-serif;
  font-size: 14px;
  line-height: 16px;
  text-rendering: optimizeLegibility;
}

a {
  text-decoration: none;
}

img {
  max-width: 100%;
  height: auto;
}
</style>
