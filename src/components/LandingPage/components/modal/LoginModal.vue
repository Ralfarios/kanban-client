<template>
  <!-- login-modal -->
  <div
    class="modal fade login-modal"
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
            <form style="display: flex; flex-direction: column">
              <div class="mb-3">
                <label for="email-login" class="form-label"
                  >Email address</label
                >
                <input type="email" class="form-control" id="email-login" />
              </div>

              <div class="mb-3">
                <label for="password-login" class="form-label">Password</label>
                <input
                  type="password"
                  class="form-control"
                  id="password-login"
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
              <span> No account? </span>

              <a href=""> Register </a>
            </div>

            <div class="separator">or</div>

            <button class="btn btn-primary">Sign in with Google</button>
          </div>

          <!-- form// -->
        </div>
      </div>
    </div>
  </div>
  <!-- login-modal/ -->
</template>

<script>
export default {
  name: 'LoginModal'
};
</script>

<style>
</style>