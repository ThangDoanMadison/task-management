<template>
  <div class="task-create">
    <div>
      <label for>Name:</label>
      <input v-model="task.name" />
    </div>
    <div>
      <label for>Status:</label>
      <!-- <input v-model="task.status" /> -->
      <select v-model="task.status">
        <option disabled value>Please select one</option>
        <option>Not started</option>
        <option>Pending</option>
        <option>In progress</option>
        <option>Delayed</option>
        <option>Done</option>
      </select>
    </div>
    <div>
      <label for>Deadline:</label>
      <input type="date" v-model="task.deadline" />
    </div>
    <div>
      <label for>Priority:</label>
      <!-- <input v-model="task.priority" /> -->
      <select v-model="task.priority">
        <option disabled value>Please select one</option>
        <option>Critical</option>
        <option>High</option>
        <option>Medium</option>
        <option>Low</option>
      </select>
    </div>
    <button @click="clickAdd">Add</button>
  </div>
</template>

<script>
export default {
  props: {
    itemEdit: {
      type: Object,
      default: null,
    },
  },
  watch: {
    itemEdit() {
      if (this.itemEdit) {
        this.task = Object.assign({}, this.itemEdit);
      } else {
        this.task = {};
      }
    },
  },
  data() {
    return {
      task: {
        id: Math.floor(Math.random() * 10000),
        name: "",
        status: "",
        deadline: "",
        priority: "",
      },
    };
  },
  methods: {
    clickAdd() {
      this.$emit("save", this.task);
      console.log(this.task);
      this.task = {
        name: "",
        status: "",
        deadline: "",
        priority: "",
      };
    },
  },
};
</script>

<style></style>
