<template>
  <!-- login-modal -->
  <div
    class="modal fade"
    id="login-modal"
    tabindex="-1"
    aria-labelledby="login-modal-label"
    aria-hidden="true"
  >
    <div
      class="modal-dialog modal-dialog-centered modal-dialog-scrollable modal-fullscreen-sm-down"
    >
      <div class="modal-content">
        <div class="modal-header">
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body">
          <h5 class="modal-title text-center" id="login-modal-label">
            Welcome back.
          </h5>

          <!-- form -->

          <div
            id="form-login"
            style="
              display: flex;
              flex-direction: column;
              margin: 36px 36px 24px 36px;
            "
            class="justify-content-center"
          >
            <!-- form-field -->
            <form
              @submit.prevent="Login"
              style="display: flex; flex-direction: column"
            >
              <div class="mb-3">
                <label for="email-login" class="form-label"
                  >Email address</label
                >
                <input
                  v-model="email"
                  type="email"
                  class="form-control"
                  id="email-login"
                />
              </div>

              <div class="mb-3">
                <label for="password-login" class="form-label">Password</label>
                <input
                  v-model="password"
                  type="password"
                  class="form-control"
                  id="password-login"
                />
              </div>

              <button
                type="submit"
                class="btn btn-dark align-self-stretch mt-2"
              >
                Login
              </button>
            </form>
            <!-- form-field// -->

            <div
              style="padding-top: 16px; padding-bottom: 8px; text-align: center"
            >
              <span> No account? </span>

              <a
                href=""
                data-bs-dismiss="modal"
                data-bs-toggle="modal"
                data-bs-target="#register-modal"
                class="switchModalAnchor"
              >
                Register
              </a>
            </div>

            <div class="separator">or</div>

            <button v-google-signin-button class="btn btn-outline-dark">
              <img
                src="https://upload.wikimedia.org/wikipedia/commons/5/53/Google_%22G%22_Logo.svg"
                style="margin-right: 24px; margin-bottom: 2px"
                width="16"
                alt=""
              />
              Sign in with Google
            </button>
          </div>

          <p class="text-center text-muted" style="font-size: 8px">
            Click "Login" to agree to Kanboard's by Ralfarios
            <a href="https://github.com/Ralfarios/kanban-client"
              >Term and Service</a
            >
            and acknowledge that Kanboard's Privacy Policy applies to you.
          </p>

          <!-- form// -->
        </div>
      </div>
    </div>
  </div>
  <!-- login-modal/ -->
</template>

<script>
import axios from "axios";
import GoogleSignInButton from "vue-google-signin-button-directive";

const baseUrl = "https://kanboard-server.herokuapp.com";

export default {
  directives: { GoogleSignInButton },
  name: "LoginModal",
  data() {
    return {
      clientId:
        "988612189787-gmff7uruop611204m9f4n5jsk7kb3roa.apps.googleusercontent.com",
      email: "",
      password: "",
    };
  },
  methods: {
    Login() {
      this.$emit("Login", {
        email: this.email,
        password: this.password,
      });
      this.email = "";
      this.password = "";
    },
    OnGoogleAuthSuccess(id_token) {
      // console.log(id_token);
      // Receive the idToken and make your magic with the backend
      axios({
        method: "POST",
        url: `${baseUrl}/glogin`,
        headers: { id_token },
      })
        .then((result) => {
          this.$emit("GoogleLogin", result.data);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    OnGoogleAuthFail(error) {
      console.log(error);
    },
  },
};
</script>

<style>
</style>