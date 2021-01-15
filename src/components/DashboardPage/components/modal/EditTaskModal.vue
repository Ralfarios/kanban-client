<template>
  <!-- edit-task-modal -->
  <div
    class="modal fade"
    id="edit-task-modal"
    tabindex="-1"
    aria-labelledby="edit-task-modal-label"
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
          <h5 class="modal-title text-center" id="edit-task-modal-label">
            Edit Task
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
              @submit.prevent="EditTaskSubmit"
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
                    <label for="title-edit" class="form-label">Title</label>
                    <input
                      v-model="populateData.title"
                      type="text"
                      class="form-control"
                      id="title-edit"
                    />
                  </div>

                  <div style="flex: 0 0 calc(50% - 0.5em)">
                    <label for="category-edit" class="form-label"
                      >Category</label
                    >
                    <select
                      v-model="populateData.category"
                      id="category-edit"
                      class="form-select"
                      aria-label="category-edit"
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
                <label for="duedate-edit" class="form-label">Due Date</label>
                <input
                  v-model="populateData.duedate"
                  type="date"
                  class="form-control"
                  id="duedate-edit"
                />
              </div>

              <div class="mb-3">
                <label for="description-edit" class="form-label"
                  >Description</label
                >
                <textarea
                  v-model="populateData.description"
                  class="form-control"
                  id="description-edit"
                  rows="3"
                ></textarea>
              </div>

              <input
                v-model="populateData.id"
                type="text"
                class="form-control"
                id="id-edit"
                style="display: none"
              />

              <button
                type="submit"
                class="btn btn-dark align-self-stretch mt-2"
              >
                Edit
              </button>
            </form>
            <!-- form-field// -->
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- edit-task-modal// -->
</template>

<script>
export default {
  name: "EditTaskModal",
  data() {
    return {
      id: "",
      title: "",
      description: "",
      category: "",
      duedate: "",
    };
  },
  props: ["populateData"],
  methods: {
    EditTaskSubmit() {
      this.$emit("EditTaskSubmit", {
        id: this.populateData.id,
        title: this.populateData.title,
        description: this.populateData.description,
        category: this.populateData.category,
        duedate: this.populateData.duedate.split("T")[0],
      });
      this.id = "";
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