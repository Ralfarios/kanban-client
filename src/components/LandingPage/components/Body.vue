<template>
  <!-- landing-body -->
  <div id="landing-body" class="landing-body">
    <div class="container-fluid">
      <div class="row landing">
        <!-- landing-typo-section -->
        <div class="col-lg-5 col-md-6 align-self-center">
          <div class="landing-typo" style="margin-left: 9.4vw">
            <h1 class="landing-typo-title">Set the same goal together!</h1>

            <p style="margin-top: 16px">
              Share your ideas for project, let your team know what you are
              doing on your project. Collaborating with your team never been
              this easier.
            </p>

            <button
              class="btn btn-outline-dark"
              data-bs-toggle="modal"
              data-bs-target="#register-modal"
            >
              Register
            </button>
          </div>
        </div>
        <!-- landing-typo-section// -->

        <!-- landing-illust-section -->
        <div class="col-lg-7 col-md-6 text-center">
          <img
            src="../../../assets/img/img_landingIllust.svg"
            alt=""
            class="d-inline-block align-top landing-illust"
          />
        </div>
        <!-- landing-illust-section// -->
      </div>
    </div>
  </div>
  <!-- landing-body// -->
</template>

<script>
export default {
  name: "LandingBody",
};
</script>

<style>
</style>