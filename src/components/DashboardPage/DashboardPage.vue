<template>
  <!-- dashboard-page -->
  <div id="dashboard-page">
    <!-- navbar -->
    <dashboard-navbar
      v-on:Logout="logout"
      :userinfo="userinfo"
    ></dashboard-navbar>
    <!-- navbar// -->

    <!-- main-page -->
    <dashboard-body :userinfo="userinfo" :task="task"></dashboard-body>
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
  props: ["userinfo", "task"],
  methods: {
    logout() {
      this.$emit("Logout");
    },
  },
};
</script>

<style>
</style>