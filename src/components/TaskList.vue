<template>
  <div class="task-list">
    <h1>Task List</h1>
    <!-- filter -->
    <div>
      <label>Filter Task</label>
      <input type="text" v-model="filterList" placeholder="Filter task...." />
    </div>
    <TaskCreate :itemEdit="taskEdit" @save="clickSave" />
    <!-- table -->
    <table id="task" class="table">
      <thead>
        <tr>
          <th></th>
          <th>Id</th>
          <th>Name</th>
          <th>Status</th>
          <th>Deadline</th>
          <th>Priority</th>
          <th>#</th>
          <th>#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in list" :key="item.id">
          <td>
            <input
              type="checkbox"
              id="checkbox"
              v-model="item.completed"
              @click="toggleCheckbox()"
            />
            <label>{{ item.completed }}</label>
          </td>
          <td>{{ item.id }}</td>
          <td>{{ item.name }}</td>
          <td
            :class="{
              'text-dark': item.status === 'Not started',
              'text-warning': item.status === 'Pending',
              'text-success': item.status === 'In progress',
              'text-danger': item.status === 'Delayed',
              'text-primary': item.status === 'Done',
            }"
          >
            {{ item.status }}
          </td>
          <td>{{ item.deadline }}</td>
          <td>{{ item.priority }}</td>
          <td>
            <div @click="clickEdit(item)">
              <i class="fas fa-edit"></i>
            </div>
          </td>
          <td>
            <div @click="clickDelete(item)">
              <i class="fa-solid fa-trash-can"></i>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import TaskCreate from "./TaskCreate";
export default {
  data() {
    return {
      filterList: "",
      taskEdit: {},
      // list data
      list: [
        {
          id: 1,
          name: "Learn Vue JS",
          status: "Not started",
          deadline: "2022-1-1",
          priority: "Critical",
          completed: true,
        },
        {
          id: 2,
          name: "Watch netflix",
          status: "Pending",
          deadline: "2022-20",
          priority: "High",
          completed: false,
        },
        {
          id: 3,
          name: "Play soccer",
          status: "In progress",
          deadline: "1-3-2022",
          priority: "Medium",
          completed: false,
        },
        {
          id: 4,
          name: "Learn guitar",
          status: "In progress",
          deadline: "1-4-2022",
          priority: "Low",
          completed: false,
        },
        {
          id: 5,
          name: "Send email",
          status: "In progress",
          deadline: "1-5-2022",
          priority: "High",
          completed: false,
        },
      ],
    };
  },
  computed: {},
  components: {
    TaskCreate,
  },
  methods: {
    toggleCheckbox() {
      if (list.completed == "true") {
        return (list.item.status = "Done");
      }
    },
    // save button funtion
    clickSave(itemSave) {
      let index = this.list.findIndex((c) => c.id === itemSave.id);
      if (index >= 0) {
        this.list.splice(index, 1, itemSave);
      } else {
        let max = 0;
        let newId = 0;
        for (let i = 0; i < this.list.length; i++) {
          if (this.list[i].id > max) {
            max = this.list[i].id;
          }
        }
        newId = max + 1;
        itemSave.id = newId;
        this.list.push(itemSave);
      }
      return;
    },
    // delete button funtion
    clickDelete(itemDelete) {
      for (let i = 0; i < this.list.length; i++) {
        if (itemDelete.id === this.list[i].id) {
          this.list.splice(i, 1);
        }
      }
    },
    // edit button funtion
    clickEdit(itemEdit) {
      console.log(itemEdit);
      this.taskEdit = itemEdit;
    },
  },
};
</script>

<style>
table {
  text-align: center;
}
#task {
  font-family: Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  width: 100%;
}
#task td,
#task th {
  border: 1px solid #ddd;
  padding: 8px;
}

#task tr:nth-child(even) {
  background-color: #f2f2f2;
}

#task tr:hover {
  background-color: #ddd;
}

#task th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: left;
  background-color: #04aa6d;
  color: white;
}
.text-danger {
  color: red;
}
.text-primary {
  color: blue;
  text-decoration-line: line-through;
}
.text-success {
  color: #04aa6d;
}
.text-warning {
  color: orange;
}
.completed {
  text-decoration-line: line-through;
}
</style>
