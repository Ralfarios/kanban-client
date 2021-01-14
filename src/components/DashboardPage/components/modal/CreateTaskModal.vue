<template>
  <!-- create-task-modal -->
  <div
    class="modal fade"
    id="create-task-modal"
    tabindex="-1"
    aria-labelledby="create-task-modal-label"
    aria-hidden="true"
  >
    <div
      class="modal-dialog modal-dialog-centered modal-dialog-scrollable modal-fullscreen-sm-down"
    >
      <div class="modal-content">
        <div class="modal-header">
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body">
          <h5 class="modal-title text-center" id="create-task-modal-label">
            Create Task
          </h5>

          <div
            id="form-register"
            style="
              display: flex;
              flex-direction: column;
              margin: 36px 36px 24px 36px;
            "
            class="justify-content-center"
          >
            <!-- form-field -->
            <form
              @submit.prevent="CreateTask"
              style="display: flex; flex-direction: column"
            >
              <div class="mb-3">
                <div
                  style="
                    display: flex;
                    flex-direction: row;
                    justify-content: space-between;
                  "
                >
                  <div style="flex: 0 0 calc(50% - 0.5em)">
                    <label for="title-add" class="form-label">Title</label>
                    <input
                      v-model="title"
                      type="text"
                      class="form-control"
                      id="title-add"
                    />
                  </div>

                  <div style="flex: 0 0 calc(50% - 0.5em)">
                    <label for="category-add" class="form-label"
                      >Category</label
                    >
                    <select
                      v-model="category"
                      id="category-add"
                      class="form-select"
                      aria-label="category-add"
                    >
                      <option selected>-- select --</option>
                      <option value="backlog">Backlog</option>
                      <option value="todo">Todo</option>
                      <option value="doing">Doing</option>
                      <option value="done">Done</option>
                    </select>
                  </div>
                </div>
              </div>

              <div class="mb-3">
                <label for="duedate-add" class="form-label">Due Date</label>
                <input
                  v-model="duedate"
                  type="date"
                  class="form-control"
                  id="duedate-add"
                />
              </div>

              <div class="mb-3">
                <label for="description-add" class="form-label"
                  >Description</label
                >
                <textarea
                  v-model="description"
                  class="form-control"
                  id="description-add"
                  rows="3"
                ></textarea>
              </div>

              <button
                type="submit"
                class="btn btn-dark align-self-stretch mt-2"
              >
                Create
              </button>
            </form>
            <!-- form-field// -->
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- create-task-modal// -->
</template>

<script>
export default {
  name: "CreateTaskModal",
  data() {
    return {
      title: "",
      description: "",
      category: "",
      duedate: "",
    };
  },
  methods: {
    CreateTask() {
      this.$emit("CreateTask", {
        title: this.title,
        description: this.description,
        category: this.category,
        duedate: this.duedate,
      });
      this.title = "";
      this.description = "";
      this.category = "";
      this.duedate = "";
    },
  },
};
</script>

<style>
</style>