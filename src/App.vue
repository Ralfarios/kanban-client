<template>
  <div class="container">
    <!-- landing-page -->
    <landing-page v-if="status === 'unsigned'"></landing-page>

    <!-- modal -->
    <register-modal
      v-if="status === 'unsigned'"
      @Register="register"
    ></register-modal>
    <login-modal v-if="status === 'unsigned'" @Login="login"></login-modal>
    <!-- modal// -->

    <!-- landing-page// -->

    <!-- dashboard-page -->
    <dashboard-page
      v-else-if="status === 'signed'"
      :userinfo="userinfo"
      :task="task"
      @Logout="logout"
    ></dashboard-page>
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
      userinfo: {},
      task: [],
    };
  },
  components: {
    DashboardPage,
    LandingPage,
    LoginModal,
    RegisterModal,
  },
  methods: {
    getTask() {
      axios({
        method: "GET",
        url: `${baseUrl}/task`,
        headers: { access_token: localStorage.getItem("access_token") },
      })
        .then(({ data }) => {
          this.task = data;
          console.log(this.task);
        })
        .catch((err) => console.log(err));
    },
    getUser() {
      axios({
        method: "GET",
        url: `${baseUrl}/getuser`,
        headers: { access_token: localStorage.getItem("access_token") },
      })
        .then(({ data }) => {
          this.userinfo = data;
        })
        .catch((err) => console.log(err));
    },
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

          this.getUser();
          this.getTask();
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

      this.getUser();
      this.getTask();
    }
  },
};
</script>

<style>
</style>