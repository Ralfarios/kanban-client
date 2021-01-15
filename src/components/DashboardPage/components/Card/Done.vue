<template>
  <div class="col-sm-6 col-md-6 col-lg-3">
    <div class="card border-success mb-3 card-parent">
      <div class="card-header text-uppercase" style="font-weight: 600">
        Done
      </div>

      <div v-for="e in task" :key="e.id" :task="task">
        <div v-if="e.category === 'done'">
          <div class="card text-white bg-success mb-3 card-content">
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

              <div>
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

              <div>
                <i class="fas fa-pen-square"></i>
                <i
                  class="fas fa-trash"
                  style="margin-left: 16px"
                  @click="deleteTask(e.id)"
                ></i>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardDone",
  props: ["task", "deleteTask"],
};
</script>

<style>
</style>