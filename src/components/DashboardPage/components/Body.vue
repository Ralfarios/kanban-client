<template>
  <div id="main-page">
    <!-- board-field -->
    <div id="board-field" class="board-field">
      <h3 class="greeting-name">Hi, {{ userinfo.firstname }}!</h3>
      <p class="greeting-project text-muted">Project: Main</p>

      <div class="container-fluid">
        <div class="row board">
          <!-- back-log -->


          <category-card
            v-for="(category, i) in categories"
            :key="i"
            :category="category"
            :editTask="editTask"
            :patchTask="patchTask"
            :deleteTask="deleteTask"
            :task="task"
          ></category-card>
        </div>
      </div>
    </div>
    <!-- board-field// -->
  </div>
</template>

<script>
// import Backlog from "./card/Backlog.vue";
// import Todo from "./card/Todo.vue";
// import Doing from "./card/Doing.vue";
// import Done from "./card/Done.vue";
import CategoryCard from "./card/CategoryCard.vue";

export default {
  name: "DashboardBody",
  props: [
    "userinfo",
    "task",
    "editTask",
    "patchTask",
    "deleteTask",
    "categories",
  ],
  components: {
    // Backlog,
    // Todo,
    // Doing,
    // Done,
    CategoryCard,
  },
};
</script>

<style>
</style>