<template>
  <div class="row my-2">
    <div class="input-group p-0 m-0">
      <div class="col-1 input-group-text">
        <input
          class="form-check"
          type="checkbox"
          :checked="task.completed"
          :disabled="task.isDisabled"
          @change="makeTaskCompleted(task)"
        />
      </div>

      <label :class="[labelClass, checkedClass]">
        {{ task.title }}
        <spinner-small v-if="task.isDisabled"></spinner-small>
      </label>

      <button
        class="col-2 btn btn-success"
        data-bs-toggle="modal"
        data-bs-target="#editModal"
        :disabled="task.isDisabled"
        @click="changeTaskEdit(task)"
      >
        Edit
      </button>

      <task-title-edit-modal></task-title-edit-modal>

      <button
        class="col-2 btn btn-danger"
        :disabled="task.isDisabled"
        @click="deleteTask(task.id)"
      >
        Delete
      </button>
    </div>
  </div>
</template>

<script>
import SpinnerSmall from "./SpinnerSmall.vue";
import TaskTitleEditModal from "./TaskTitleEditModal.vue";
import { mapActions, mapMutations } from "vuex";

export default {
  components: { SpinnerSmall, TaskTitleEditModal },

  data() {
    return {
      labelClass:
        "col-7 bg-primary p-3 bg-opacity-75 fw-bold fs-5 text-uppercase text-start",
    };
  },

  props: {
    task: {
      type: Object,
      required: true,
    },
  },

  methods: {
    ...mapActions(["deleteTask", "makeTaskCompleted"]),
    ...mapMutations(["changeTaskEdit"]),
  },

  computed: {
    checkedClass() {
      return this.task.completed
        ? "bg-warning text-decoration-line-through"
        : "";
    },
  },
};
</script>

<style></style>
