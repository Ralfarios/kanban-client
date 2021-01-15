<template>
  <div class="col-sm-6 col-md-6 col-lg-3">
    <div :class="ColorCategory">
      <div class="card-header text-uppercase" style="font-weight: 600">
        {{ category }}
      </div>

      <task-card
        v-for="e in task"
        :key="e.id"
        :task="task"
        :editTask="editTask"
        :patchTask="patchTask"
        :deleteTask="deleteTask"
        :category="category"
        :e="e"
      ></task-card>
    </div>
  </div>
</template>

<script>
import TaskCard from "./TaskCard.vue";

export default {
  name: "CategoryCard",
  props: ["task", "editTask", "patchTask", "deleteTask", "category"],
  data() {
    return {
      colorCategory: [
        "card border-secondary mb-3 card-parent",
        "card border-primary mb-3 card-parent",
        "card border-warning mb-3 card-parent",
        "card border-success mb-3 card-parent",
      ],
    };
  },
  components: {
    TaskCard,
  },
  computed: {
    ColorCategory() {
      let style;

      switch (this.category) {
        case "backlog":
          style = this.colorCategory[0];
          break;
        case "todo":
          style = this.colorCategory[1];
          break;
        case "doing":
          style = this.colorCategory[2];
          break;
        case "done":
          style = this.colorCategory[3];
          break;
        default:
          style = this.colorCategory[0];
          break;
      }

      return style;
    },
  },
};
</script>

<style>
</style>