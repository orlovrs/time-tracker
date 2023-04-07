<template>
  <div id="app" class="container">
    <h1 class="mt-3 mb-3">Task planner</h1>
    <CreateTask @new-task="createTaskCard" />
    <br/>
    <h1 class="mb-3">Your Tasks</h1>
    <TaskCard
      class="mb-3"
      v-for="task in tasks"
      :key="task.id"
      :id="task.id"
      :taskName="task.name"
      :timeSpent="task.timeSpent"
      :plannedDate="task.plannedDate"
      :estimation="Number(task.estimation)"
      :status="task.status"
      @delete-task="deleteTaskCard" />
  </div>
</template>

<script>
import CreateTask from "@/components/CreateTask.vue";
import TaskCard from "@/components/TaskCard.vue";

export default {
  components: {
    CreateTask,
    TaskCard,
  },
  data() {
    return {
      tasks: [],
      nextTaskId: 1,
    };
  },
  methods: {
    createTaskCard(taskDetails) {
      this.tasks.push({
        id: this.nextTaskId++,
        name: taskDetails.name,
        plannedDate: taskDetails.plannedDate,
        estimation: taskDetails.estimation,
        timeSpent: taskDetails.timeSpent,
        status: taskDetails.status
      });
    },
    deleteTaskCard(id) {
      console.log(id)
      this.tasks = this.tasks.filter(t => t.id != id)
    },
  },
};
</script>>