<template>
  <div class="col-sm-6 col-md-6 col-lg-3">
    <div class="card border-warning mb-3 card-parent">
      <div class="card-header text-uppercase" style="font-weight: 600">
        Doing
      </div>

      <div class="card text-white bg-warning mb-3 card-content">
        <div
          class="card-header"
          style="
            background-color: transparent;
            border: 0;
            font-weight: 600;
            padding: 8px 16px 2px 16px;
          "
        >
          #Title
        </div>

        <div class="card-body" style="padding: 2px 16px 8px 16px">
          <p class="card-text">#description</p>

          <div>
            <p
              class="card-text fst-italic fw-bold small"
              style="margin-top: -6px"
            >
              John Doe
            </p>
            <p class="card-text fst-italic date-task small">2021 01 30</p>
          </div>

          <div>
            <i class="fas fa-pen-square"></i>
            <i class="fas fa-trash" style="margin-left: 16px"></i>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardDoing",
};
</script>

<style>
</style>