<template>
  <!-- register-modal -->
  <div
    class="modal fade register-modal"
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
            <form style="display: flex; flex-direction: column">
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
                <input type="email" class="form-control" id="email-register" />
              </div>

              <div class="mb-3">
                <label for="password-register" class="form-label"
                  >Password</label
                >
                <input
                  type="password"
                  class="form-control"
                  id="password-register"
                />
              </div>

              <button
                type="submit"
                class="btn btn-primary align-self-stretch mt-2"
              >
                Submit
              </button>
            </form>
            <!-- form-field// -->

            <div
              style="padding-top: 16px; padding-bottom: 8px; text-align: center"
            >
              <span> Already have? </span>

              <a href=""> Sign in </a>
            </div>
          </div>

          <!-- form// -->
        </div>
      </div>
    </div>
  </div>
  <!-- register-modal// -->
</template>

<script>
export default {
  name: 'RegisterModal'
};
</script>

<style>
</style>