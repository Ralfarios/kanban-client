<template>
      <!-- landing-navbar -->
    <nav class="navbar sticky-top navbar-light nav-container">
      <div class="container-fluid">
        <!-- logo-section -->
        <div class="logo-section">
          <!-- logo-image -->
          <a class="navbar-brand">
            <img
              style="margin-top: 4px"
              src="../../../assets/img/img_logoB.svg"
              alt=""
              height="24"
              class="d-inline-block align-top"
            />
          </a>
          <!-- logo-image// -->
        </div>
        <!-- logo-section// -->

        <!-- landing-btn-section -->
        <div id="landing-btn-section" class="btn-group">
          <button
            id="register-nav"
            class="btn btn-outline-dark btn-sm btn-landing-nav"
            style="
              color: black;
              margin-right: 18px;
              border-radius: 4px;
              text-decoration: none;
              font-weight: 400;
            "
            data-bs-toggle="modal"
            data-bs-target="#register-modal"
          >
            Register
          </button>

          <button
            id="login-nav"
            class="btn btn-dark btn-sm btn-landing-login-nav"
            style="border-radius: 4px"
            data-bs-toggle="modal"
            data-bs-target="#login-modal"
          >
            Login
          </button>
        </div>
        <!-- landing-btn-section// -->
      </div>
    </nav>
    <!-- landing-navbar// -->
</template>

<script>
export default {
  name: 'LandingNavbar'
}
</script>

<style>

</style>