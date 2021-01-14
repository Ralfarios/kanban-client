<template>
  <!-- landing-page -->
  <div id="landing-page">
    <!-- landing-navbar -->
    <landing-navbar></landing-navbar>
    <!-- landing-navbar// -->

    <!-- landing-body -->
    <landing-body></landing-body>
    <!-- landing-body// -->
  </div>
  <!-- landing-page// -->
</template>

<script>
import LandingBody from './components/Body.vue';
import LandingNavbar from './components/Navbar.vue';

export default {
  name: 'LandingPage',
  components: {
    LandingNavbar,
    LandingBody
  },
};
</script>

<style>
</style>