<template>
  <div id="main-page">
    <!-- board-field -->
    <div id="board-field" class="board-field">
      <h3 class="greeting-name">Hi #FIRSTNAME</h3>
      <p class="greeting-project text-muted">#PROJECTNAME</p>

      <div class="container-fluid">
        <div class="row board">
          <!-- back-log -->
          <backlog></backlog>
          <!-- back-log// -->

          <!-- todo -->
          <todo></todo>
          <!-- todo// -->

          <!-- doing -->
          <doing></doing>
          <!-- doing// -->

          <!-- done -->
          <done></done>
          <!-- done// -->
        </div>
      </div>
    </div>
    <!-- board-field// -->
  </div>
</template>

<script>
import Backlog from "./Card/Backlog.vue";
import Todo from "./Card/Todo.vue";
import Doing from "./Card/Doing.vue";
import Done from "./Card/Done.vue";

export default {
  name: "DashboardBody",
  components: {
    Backlog,
    Todo,
    Doing,
    Done,
  },
};
</script>

<style>
</style>