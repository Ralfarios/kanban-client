<template>
  <!-- dashboard-page -->
  <div id="dashboard-page">
    <!-- navbar -->
    <dashboard-navbar @Logout="logout" :userinfo="userinfo"></dashboard-navbar>
    <!-- navbar// -->

    <!-- main-page -->
    <dashboard-body
      :editTask="editTask"
      :patchTask="patchTask"
      :deleteTask="deleteTask"
      :userinfo="userinfo"
      :categories="categories"
      :task="task"
    ></dashboard-body>
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
  props: [
    "userinfo",
    "task",
    "editTask",
    "patchTask",
    "deleteTask",
    "categories",
  ],
  methods: {
    logout() {
      this.$emit("Logout");
    },
  },
};
</script>

<style>
</style>