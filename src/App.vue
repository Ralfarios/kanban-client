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
      :editTask="editTask"
      :patchTask="patchTask"
      :deleteTask="deleteTask"
      @Logout="logout"
    ></dashboard-page>

    <!-- modal -->
    <create-task-modal @CreateTask="createTask"></create-task-modal>
    <!-- <edit-task-modal @editTask="edit"></edit-task-modal> -->
    <edit-task-modal
      :editTask="editTask"
      @EditTaskSubmit="editTaskSubmit"
      :populateData="populateData"
    ></edit-task-modal>
    <patch-task-modal
      :patchTask="patchTask"
      @PatchTaskSubmit="patchTaskSubmit"
      :populateData="populateData"
    ></patch-task-modal>
    <!-- modal// -->
    <!-- dashboard-page// -->
  </div>
</template>

<script>
import axios from "axios";
import DashboardPage from "./components/DashboardPage/DashboardPage.vue";
import LandingPage from "./components/LandingPage/LandingPage.vue";
import LoginModal from "./components/LandingPage/components/modal/LoginModal.vue";
import RegisterModal from "./components/LandingPage/components/modal/RegisterModal.vue";
import CreateTaskModal from "./components/DashboardPage/components/modal/CreateTaskModal.vue";
import EditTaskModal from "./components/DashboardPage/components/modal/EditTaskModal.vue";
import PatchTaskModal from "./components/DashboardPage/components/modal/PatchTaskModal.vue";

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
      populateData: {
        id: "",
        title: "",
        description: "",
        duedate: "",
        category: "",
      },
    };
  },
  components: {
    DashboardPage,
    LandingPage,
    LoginModal,
    RegisterModal,
    CreateTaskModal,
    EditTaskModal,
    PatchTaskModal,
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
        })
        .catch((err) => console.log(err));
    },
    createTask(value) {
      axios({
        method: "POST",
        url: `${baseUrl}/task`,
        headers: { access_token: localStorage.getItem("access_token") },
        data: {
          title: value.title,
          description: value.description,
          duedate: value.duedate,
          category: value.category,
        },
      })
        .then(({ data }) => {
          console.log(data);
          $("#create-task-modal").modal("toggle");
          this.getTask();
        })
        .catch((err) => {
          console.log(err);
        });
    },
    editTask(id) {
      axios({
        method: "GET",
        url: `${baseUrl}/task/${id}`,
        headers: { access_token: localStorage.getItem("access_token") },
      })
        .then(({ data }) => {
          $("#edit-task-modal").modal("toggle");
          this.populateData.id = data.id;
          this.populateData.title = data.title;
          this.populateData.description = data.description;
          this.populateData.duedate = data.duedate.split("T")[0];
          this.populateData.category = data.category;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    editTaskSubmit(value) {
      // console.log(value);
      axios({
        method: "PUT",
        url: `${baseUrl}/task/${value.id}`,
        headers: { access_token: localStorage.getItem("access_token") },
        data: {
          title: value.title,
          description: value.description,
          duedate: value.duedate,
          category: value.category,
        },
      })
        .then(({ data }) => {
          // console.log(data);
          $("#edit-task-modal").modal("toggle");
          this.getTask();
        })
        .catch((err) => console.log(err));
    },
    patchTask(id) {
      axios({
        method: "GET",
        url: `${baseUrl}/task/${id}`,
        headers: { access_token: localStorage.getItem("access_token") },
      })
        .then(({ data }) => {
          // console.log(data); // デバッグ用
          $("#patch-task-modal").modal("toggle");
          this.populateData.id = data.id;
          this.populateData.category = data.category;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    patchTaskSubmit(value) {
      // console.log(value); // デバッグ用
      axios({
        method: "PATCH",
        url: `${baseUrl}/task/${value.id}`,
        headers: { access_token: localStorage.getItem("access_token") },
        data: {
          title: value.title,
          category: value.category,
        },
      })
        .then(({ data }) => {
          // console.log(data);
          $("#patch-task-modal").modal("toggle");
          this.getTask();
        })
        .catch((err) => {
          console.log(err);
        });
    },
    deleteTask(id) {
      // console.log(id)
      axios({
        method: "DELETE",
        url: `${baseUrl}/task/${id}`,
        headers: { access_token: localStorage.getItem("access_token") },
      })
        .then(({ data }) => {
          console.log(data.message);
          this.getTask();
        })
        .catch((err) => {
          console.log(err);
        });
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