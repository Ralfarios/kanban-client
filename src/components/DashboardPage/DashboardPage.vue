<template>
  <!-- dashboard-page -->
  <div id="dashboard-page">
    <!-- navbar -->
    <dashboard-navbar v-on:Logout="logout"></dashboard-navbar>
    <!-- navbar// -->

    <!-- main-page -->
    <dashboard-body></dashboard-body>
    <!-- main-page// -->
  </div>
  <!-- dashboard-page// -->
</template>

<script>
import DashboardBody from "./components/Body.vue";
import DashboardNavbar from "./components/Navbar.vue";

export default {
  name: "DashboardPage",
  components: {
    DashboardBody,
    DashboardNavbar,
  },
  methods: {
    logout() {
      this.$emit("Logout");
    },
  },
};
</script>

<style>
</style>