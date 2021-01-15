<template>
  <div class="container">
    <!-- landing-page -->
    <landing-page v-if="status === 'unsigned'"></landing-page>

    <!-- modal -->
    <register-modal
      v-if="status === 'unsigned'"
      @Register="register"
    ></register-modal>
    <login-modal
      v-if="status === 'unsigned'"
      @Login="login"
      @GoogleLogin="GoogleLogin"
    ></login-modal>
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
      :categories="categories"
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
import Swal from "sweetalert2";

const baseUrl = "https://kanboard-server.herokuapp.com";

export default {
  name: "App",
  data() {
    return {
      message: "Hello world",
      status: "unsigned",
      statreg: "",
      userinfo: {},
      task: [],
      categories: ["backlog", "todo", "doing", "done"],
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
      Swal.queue([
        {
          title: "Now loading...",
          text: "Keep calm, because we are fetching your data!",
          showConfirmButton: false,
          onOpen: () => {
            Swal.showLoading();
            return axios({
              method: "GET",
              url: `${baseUrl}/task`,
              headers: { access_token: localStorage.getItem("access_token") },
            })
              .then(({ data }) => {
                this.task = data;
                Swal.close();
              })
              .catch((err) => console.log(err));
          },
        },
      ]);
    },
    createTask(value) {
      Swal.queue([
        {
          title: "Creating Task ...",
          showConfirmButton: false,
          onOpen: () => {
            Swal.showLoading();
            return axios({
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
                // console.log(data);
                $("#create-task-modal").modal("toggle");
                Swal.close();
                this.getTask();
              })
              .catch((err) => {
                const errMsg = err.response.data.message;
                Swal.fire({
                  icon: "error",
                  title: "Oops...",
                  text: errMsg,
                });
              });
          },
        },
      ]);
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
          const errMsg = err.response.data.message;
          Swal.fire({
            icon: "error",
            title: "Oops...",
            text: errMsg,
          });
        });
    },
    editTaskSubmit(value) {
      // console.log(value);
      Swal.queue([
        {
          title: "Editing Task ...",
          showConfirmButton: false,
          onOpen: () => {
            Swal.showLoading();
            return axios({
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
                Swal.close();
                this.getTask();
              })
              .catch((err) => {
                const errMsg = err.response.data.message;
                Swal.fire({
                  icon: "error",
                  title: "Oops...",
                  text: errMsg,
                });
              });
          },
        },
      ]);
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
          const errMsg = err.response.data.message;
          Swal.fire({
            icon: "error",
            title: "Oops...",
            text: errMsg,
          });
        });
    },
    patchTaskSubmit(value) {
      // console.log(value); // デバッグ用
      Swal.queue([
        {
          title: "Editing Task ...",
          showConfirmButton: false,
          onOpen: () => {
            Swal.showLoading();
            return axios({
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
                Swal.close();
                this.getTask();
              })
              .catch((err) => {
                const errMsg = err.response.data.message;
                Swal.fire({
                  icon: "error",
                  title: "Oops...",
                  text: errMsg,
                });
              });
          },
        },
      ]);
    },
    deleteTask(id) {
      Swal.fire({
        title: "Are you sure?",
        text: "You won't be able to revert this!",
        icon: "warning",
        showCancelButton: true,
        confirmButtonColor: "#3085d6",
        cancelButtonColor: "#d33",
        confirmButtonText: "Yes, delete it!",
      }).then((result) => {
        if (result.isConfirmed) {
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
              const errMsg = err.response.data.message;
              Swal.fire({
                icon: "error",
                title: "Oops...",
                text: errMsg,
              });
            });
        }
      });
      // console.log(id)
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
      Swal.queue([
        {
          title: "Now loading...",
          text: "We are creating your account right now!",
          showConfirmButton: false,
          onOpen: () => {
            Swal.showLoading();
            return axios({
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
                Swal.fire({
                  icon: "success",
                  title: "Account created!",
                  text:
                    "Your account has been created successfully. Let's login!",
                });
                $("#register-modal").modal("toggle");
                $("#login-modal").modal("toggle");
              })
              .catch((err) => {
                const errMsg = err.response.data.message;
                Swal.fire({
                  icon: "error",
                  title: "Oops...",
                  text: errMsg,
                });
              });
          },
        },
      ]);
    },
    login(value) {
      // console.log(value); //デバッグ用
      Swal.queue([
        {
          title: "Now loading...",
          text: "Get your coffee because we are logging in you up!",
          showConfirmButton: false,
          onOpen: () => {
            Swal.showLoading();
            return axios({
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
                Swal.close();
              })
              .catch((err) => {
                const errMsg = err.response.data.message;
                Swal.fire({
                  icon: "error",
                  title: "Oops...",
                  text: errMsg,
                });
              });
          },
        },
      ]);
    },
    GoogleLogin(value) {
      $("#login-modal").modal("toggle");
      this.status = "signed";
      localStorage.setItem("access_token", value.access_token);

      this.getUser();
      this.getTask();
    },
    logout() {
      Swal.fire({
        title: "Are you sure?",
        text: "We will miss you!",
        icon: "warning",
        showCancelButton: true,
        confirmButtonColor: "#3085d6",
        cancelButtonColor: "#d33",
        confirmButtonText: "Yes, log me out!",
        cancelButtonText: "No, I wanna stay!",
      }).then((result) => {
        if (result.isConfirmed) {
          Swal.close();
          localStorage.clear();
          this.status = "unsigned";
        }
      });
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