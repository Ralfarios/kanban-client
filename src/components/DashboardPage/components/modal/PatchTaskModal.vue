<template>
  <!-- patch-task-modal -->
  <div
    class="modal fade"
    id="patch-task-modal"
    tabindex="-1"
    aria-labelledby="patch-task-modal-label"
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
          <h5 class="modal-title text-center" id="patch-task-modal-label">
            Select Category
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
              @submit.prevent="PatchTaskSubmit"
              style="display: flex; flex-direction: column"
            >
              <div class="mb-3">
                <label for="category-edit" class="form-label">Category</label>
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
  <!-- patch-task-modal// -->
</template>

<script>
export default {
  name: "PatchTaskModal",
  data() {
    return {
      id: "",
      category: "",
    };
  },
  props: ["populateData"],
  methods: {
    PatchTaskSubmit() {
      this.$emit("PatchTaskSubmit", {
        id: this.populateData.id,
        category: this.populateData.category,
      });
      this.id = "";
      this.category = "";
    },
  },
};
</script>

<style>
</style>