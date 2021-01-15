<template>
  <!-- register-modal -->
  <div
    class="modal fade"
    id="register-modal"
    tabindex="-1"
    aria-labelledby="register-modal-label"
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
          <h5 class="modal-title text-center" id="register-modal-label">
            Join Kanboard.
          </h5>

          <!-- form -->

          <div
            id="form-register"
            style="
              display: flex;
              flex-direction: column;
              margin: 36px 36px 24px 36px;
            "
            class="justify-content-center"
          >
            <!-- form-field -->
            <form
              @submit.prevent="Register"
              style="display: flex; flex-direction: column"
            >
              <div class="mb-3">
                <div
                  style="
                    display: flex;
                    flex-direction: row;
                    justify-content: space-between;
                  "
                >
                  <div style="flex: 0 0 calc(50% - 0.5em)">
                    <label for="firstname-register" class="form-label"
                      >First Name</label
                    >
                    <input
                      v-model="firstname"
                      type="text"
                      class="form-control"
                      id="firstname-register"
                    />
                  </div>
                  <div style="flex: 0 0 calc(50% - 0.5em)">
                    <label for="lastname-register" class="form-label"
                      >Last Name</label
                    >
                    <input
                      v-model="lastname"
                      type="text"
                      class="form-control"
                      id="lastname-register"
                    />
                  </div>
                </div>
              </div>

              <div class="mb-3">
                <label for="email-register" class="form-label"
                  >Email address</label
                >
                <input
                  v-model="email"
                  type="email"
                  class="form-control"
                  id="email-register"
                />
              </div>

              <div class="mb-3">
                <label for="password-register" class="form-label"
                  >Password</label
                >
                <input
                  v-model="password"
                  type="password"
                  class="form-control"
                  id="password-register"
                />
              </div>

              <button
                type="submit"
                class="btn btn-dark align-self-stretch mt-2"
              >
                Register
              </button>
            </form>
            <!-- form-field// -->

            <div
              style="padding-top: 16px; padding-bottom: 8px; text-align: center"
            >
              <span> Already have? </span>

              <a
                href=""
                data-bs-dismiss="modal"
                data-bs-toggle="modal"
                data-bs-target="#login-modal"
                class="switchModalAnchor"
              >
                Login
              </a>
            </div>
          </div>

          <p class="text-center text-muted" style="font-size: 8px; ">
            Click “Register” to agree to Kanboard's by Ralfarios <a href="https://github.com/Ralfarios/kanban-client">Term and Service</a> and
            acknowledge that Kanboard's Privacy Policy applies to you.
          </p>

          <!-- form// -->
        </div>
      </div>
    </div>
  </div>
  <!-- register-modal// -->
</template>

<script>
export default {
  name: "RegisterModal",
  data() {
    return {
      firstname: "",
      lastname: "",
      email: "",
      password: "",
    };
  },
  methods: {
    Register() {
      this.$emit("Register", {
        firstname: this.firstname,
        lastname: this.lastname,
        email: this.email,
        password: this.password,
      });
      this.firstname = "";
      this.lastname = "";
      this.email = "";
      this.password = "";
    },
  },
};
</script>

<style>
</style>