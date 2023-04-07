<template>
    <div class="row align-items-end">
      <div class="col-md-4">
        <div class="form-group">
          <label for="taskName">Task Name</label>
          <input type="text" class="form-control" id="taskName" v-model="name" />
        </div>
      </div>
      <div class="col-md-2">
        <div class="form-group">
          <label for="plannedDate">Planned Date</label>
          <input type="date" class="form-control" id="plannedDate" v-model="plannedDate" />
        </div>
      </div>
      <div class="col-md-2">
        <div class="form-group">
          <label for="estimation">Estimation (in minutes)</label>
          <input type="number" class="form-control" id="estimation" v-model="estimation" />
        </div>
      </div>
      <div class="col-md-4">
        <button type="button" class="btn btn-primary mt-5 mt-md-0" @click="createTask">Create Task</button>
      </div>
  </div>
</template>
  
  <script>
  export default {
    name: "NewTaskCard",
    data() {
      return {
        name: "",
        plannedDate: "",
        estimation: "",
      };
    },
    methods: {
      createTask() {
        this.$emit("new-task", {
          name: this.name,
          status: 'waiting',
          estimation: this.estimation,
          timeSpent: 0,
          plannedDate: this.plannedDate,
        });
  
        // Reset the input fields
        this.name = "";
        this.plannedDate = "";
        this.estimation = "";
      },
    },
  };
  </script>