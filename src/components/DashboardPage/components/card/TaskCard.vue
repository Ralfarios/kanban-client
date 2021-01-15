<template>
  <div>
    <div v-if="e.category === category">
      <div :class="ColorCategory">
        <div
          class="card-header"
          style="
            background-color: transparent;
            border: 0;
            font-weight: 600;
            padding: 8px 16px 2px 16px;
          "
        >
          {{ e.title }}
        </div>
        <div class="card-body" style="padding: 2px 16px 8px 16px">
          <p class="card-text">{{ e.description }}</p>

          <div id="task-info">
            <p
              class="card-text fst-italic fw-bold small"
              style="margin-top: -6px"
            >
              {{ e.User.firstname }} {{ e.User.lastname }}
            </p>
            <p class="card-text fst-italic date-task small">
              {{ e.duedate.split("T")[0] }}
            </p>
          </div>

          <div id="task-btn-action" class="task-btn-action">
            <i
              class="fas fa-pen-square btn-action-hov"
              @click="editTask(e.id)"
            ></i>
            <i
              class="fas fa-arrows-alt btn-action-hov"
              style="margin-left: 16px"
              @click="patchTask(e.id)"
            ></i>
            <i
              class="fas fa-trash btn-action-hov"
              style="margin-left: 16px"
              @click="deleteTask(e.id)"
            ></i>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TaskCard",
  props: ["e", "task", "editTask", "patchTask", "deleteTask", "category"],
  data() {
    return {
      color: [
        "card text-white bg-dark mb-3 card-content",
        "card text-white bg-primary mb-3 card-content",
        "card text-white bg-warning mb-3 card-content",
        "card text-white bg-success mb-3 card-content",
      ],
    };
  },
  computed: {
    ColorCategory() {
      let style;

      switch (this.category) {
        case "backlog":
          style = this.color[0];
          break;
        case "todo":
          style = this.color[1];
          break;
        case "doing":
          style = this.color[2];
          break;
        case "done":
          style = this.color[3];
          break;
        default:
          style = this.color[0];
          break;
      }

      return style;
    },
  },
};
</script>

<style>
</style>