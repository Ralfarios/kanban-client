<template>
  <div class="container">
    <!-- landing-page -->
    <landing-page v-if="status === 'unsigned'"></landing-page>

    <!-- modal -->
    <register-modal
      v-if="status === 'unsigned'"
      v-on:Register="register"
    ></register-modal>
    <login-modal v-if="status === 'unsigned'" v-on:Login="login"></login-modal>
    <!-- modal// -->

    <!-- landing-page// -->

    <!-- dashboard-page -->
    <dashboard-page v-else-if="status === 'signed'" v-on:Logout="logout"></dashboard-page>
    <!-- dashboard-page// -->
  </div>
</template>

<script>
import axios from "axios";
import DashboardPage from "./components/DashboardPage/DashboardPage.vue";
import LandingPage from "./components/LandingPage/LandingPage.vue";
import LoginModal from "./components/LandingPage/components/modal/LoginModal.vue";
import RegisterModal from "./components/LandingPage/components/modal/RegisterModal.vue";

const baseUrl = "http://localhost:3000";

export default {
  name: "App",
  data() {
    return {
      message: "Hello world",
      status: "unsigned",
      statreg: "",
    };
  },
  components: {
    DashboardPage,
    LandingPage,
    LoginModal,
    RegisterModal,
  },
  methods: {
    register(value) {
      // console.log(value); //　デバッグ用

      axios({
        method: "POST",
        url: `${baseUrl}/register`,
        data: {
          firstname: value.firstname,
          lastname: value.lastname,
          email: value.email,
          password: value.password,
        },
      })
        .then((result) => {
          $("#register-modal").modal("toggle");
          $("#login-modal").modal("toggle");
        })
        .catch((err) => {
          console.log(err);
        });
    },
    login(value) {
      // console.log(value); //デバッグ用

      axios({
        method: "POST",
        url: `${baseUrl}/login`,
        data: {
          email: value.email,
          password: value.password,
        },
      })
        .then(({ data }) => {
          $("#login-modal").modal("toggle");
          this.status = "signed";
          localStorage.setItem("access_token", data.access_token);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    logout() {
      localStorage.clear();
      this.status = "unsigned";
    },
  },
  created() {
    if (localStorage.getItem("access_token")) {
      this.status = "signed";
    }
  },
};
</script>

<style>
</style>