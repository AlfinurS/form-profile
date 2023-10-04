<template>
  <div id="app">
    <main>
      <MainPageComponent></MainPageComponent>
    </main>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import MainPageComponent from "@/components/MainPageComponent.vue";
export default defineComponent({
  name: "App",
  components: {
    MainPageComponent,
  },
});
</script>

<style lang="scss" scoped>
@import "@/assets/scss/style.scss";
</style>
