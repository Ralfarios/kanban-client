<template>
  <div id="main-page">
    <!-- board-field -->
    <div id="board-field" class="board-field">
      <h3 class="greeting-name">Hi, {{ userinfo.firstname }}!</h3>
      <p class="greeting-project text-muted">Project: Main</p>

      <div class="container-fluid">
        <div class="row board">
          <!-- back-log -->
          <backlog
            :editTask="editTask"
            :patchTask="patchTask"
            :deleteTask="deleteTask"
            :task="task"
          ></backlog>
          <!-- back-log// -->

          <!-- todo -->
          <todo
            :editTask="editTask"
            :patchTask="patchTask"
            :deleteTask="deleteTask"
            :task="task"
          ></todo>
          <!-- todo// -->

          <!-- doing -->
          <doing
            :editTask="editTask"
            :patchTask="patchTask"
            :deleteTask="deleteTask"
            :task="task"
          ></doing>
          <!-- doing// -->

          <!-- done -->
          <done
            :editTask="editTask"
            :patchTask="patchTask"
            :deleteTask="deleteTask"
            :task="task"
          ></done>
          <!-- done// -->
        </div>
      </div>
    </div>
    <!-- board-field// -->
  </div>
</template>

<script>
import Backlog from "./card/Backlog.vue";
import Todo from "./card/Todo.vue";
import Doing from "./card/Doing.vue";
import Done from "./card/Done.vue";

export default {
  name: "DashboardBody",
  props: ["userinfo", "task", "editTask", "patchTask", "deleteTask"],
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