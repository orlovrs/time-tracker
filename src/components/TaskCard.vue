<template>
  <div class="card">
    <div class="card-header">
      {{ taskName }}
    </div>
    <div class="card-body">
      <h5 class="card-title">Status: {{ status }}</h5>
      <p class="card-text">Estimation, minutes: {{ estimation }}</p>
      <p class="card-text">Time Spent: {{ getTimeFromDuration() }}</p>
      <p class="card-text">Planned Date: {{ plannedDate }}</p>
      <div class="btn-group" role="group">
        <button
          type="button"
          class="btn btn-success"
          @click="startTask"
          :disabled="isStarted || isDone">{{startButtonLabel}}</button>
        <button
          type="button"
          class="btn btn-warning"
          @click="pauseTask"
          :disabled="!isStarted || isDone">Pause</button>
        <button
          type="button"
          class="btn btn-primary"
          @click="doneTask"
          :disabled="!isStarted || isDone">Done</button>
        <button
          type="button"
          class="btn btn-danger"
          @click="deleteTask"
          :disabled="isDone">Delete</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TaskCard",
  props: {
    id: Number,
    taskName: String,
    status: String,
    estimation: Number,
    timeSpent: Number,
    plannedDate: String,
  },
  data() {
    return {
      executionDuration: 0,
      isStarted: false,
      isDone: false,
      interval: null
    }
  },
  computed: {
    startButtonLabel() {
      return this.isStarted ? this.getTimeFromDuration() : 'Start'
    }
  },
  methods: {
    startTask() {
      this.interval = setInterval(() => {
        this.executionDuration++;
      }, 1000);
      this.isStarted = true;
      this.status = 'in progress';
    },
    pauseTask() {
      clearInterval(this.interval);
      this.isStarted = false;
      this.status = 'waiting';
    },
    doneTask() {
      clearInterval(this.interval);
      this.isStarted = false;
      this.isDone = true;
      this.status = 'done';
    },
    deleteTask() {
      clearInterval(this.interval);
      this.$emit("delete-task", this.id);
    },
    getTimeFromDuration() {
      let seconds = Math.floor((this.executionDuration) % 60);
      let minutes = Math.floor((this.executionDuration) / 60);
      return `${minutes < 10 ? '0' + minutes : minutes}:${seconds < 10 ? '0' + seconds : seconds}`
    }
  }
};
</script>