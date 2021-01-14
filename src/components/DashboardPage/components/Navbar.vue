<template>
  <nav class="navbar sticky-top navbar-light nav-container">
    <div class="container-fluid">
      <!-- logo-section -->
      <div class="logo-section">
        <!-- logo-image -->
        <a id="logo-image" class="navbar-brand">
          <img
            src="../../../assets/img/img_logoB.svg"
            alt=""
            height="32"
            class="d-inline-block align-top"
          />
        </a>
        <!-- logo-image// -->

        <!-- logo-separator -->
        <div class="logo-separator"></div>
        <!-- logo-separator// -->

        <!-- logo-greeting -->
        <div id="logo-greeting">
          <h5 class="logo-greeting">Good Afternoon</h5>
        </div>
        <!-- logo-greeting// -->
      </div>
      <!-- logo-section// -->

      <!-- user-section -->
      <div id="user-section" class="btn-group">
        <button
          id="create-task-btn-nav"
          class="btn btn-success btn-sm btn-nav"
          style="margin-right: 18px; border-radius: 4px"
        >
          Project
        </button>
        <button
          id="project-btn-nav"
          class="btn btn-primary btn-sm btn-nav"
          style="margin-right: 36px; border-radius: 4px"
        >
          Create task
        </button>

        <!-- user-image -->
        <a
          id="user-image"
          href=""
          data-bs-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          <img
            src="https://thumbs.dreamstime.com/b/default-avatar-profile-vector-user-profile-default-avatar-profile-vector-user-profile-profile-179376714.jpg"
            alt=""
            class="user-prof-pic"
          />
        </a>
        <!-- user-image// -->

        <!-- user-info-section -->
        <div class="dropdown-menu dropdown-menu-end">
          <!-- user-info -->
          <div id="user-info">
            <h6 class="dropdown-header user-info-name">John Doe</h6>
            <h6 class="dropdown-header user-info-mail">johndoe@mail.com</h6>
          </div>
          <!-- user-info// -->

          <div class="dropdown-divider"></div>

          <a id="create-task-drop" class="dropdown-item btn-drop" href=""
            >Create task</a
          >
          <a id="project-drop" class="dropdown-item btn-drop" href=""
            >Project</a
          >

          <div class="dropdown-divider btn-drop"></div>

          <a id="logout-btn" class="dropdown-item" href="">Logout</a>
        </div>
        <!-- user-info-section// -->
      </div>
      <!-- user-section// -->
    </div>
  </nav>
</template>

<script>
export default {
  name: "DashboardNavbar",
};
</script>

<style>
</style>