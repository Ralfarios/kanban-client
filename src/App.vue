<template>
  <div class="container">
    <!-- landing-page -->
    <landing-page></landing-page>
    <!-- landing-page// -->

    <!-- dashboard-page -->
    <!-- <dashboard-page></dashboard-page> -->
    <!-- dashboard-page// -->
  </div>
</template>

<script>
import DashboardPage from "./components/DashboardPage/DashboardPage.vue";
import LandingPage from "./components/LandingPage/LandingPage.vue";

export default {
  name: "App",
  data() {
    return {
      message: "Hello world",
    };
  },
  components: {
    DashboardPage,
    LandingPage,
  },
};
</script>

<style>
</style>