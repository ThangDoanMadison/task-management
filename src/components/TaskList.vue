<template>
  <h1>Task List</h1>
  <div class="search-wrapper">
    <label>Search title:</label>
    <input type="text" v-model="search" placeholder="Search title.." />
  </div>
  <TaskCreate :itemEdit="taskEdit" @save="clickSave" />
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
          <input type="checkbox" id="checkbox" v-model="checked" />
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
</template>
<script>
import TaskCreate from "./TaskCreate";
export default {
  computed: {
    filteredList() {
      return this.list.filter((item) => {
        return item.name.toLowerCase().includes(this.search.toLowerCase());
      });
    },
  },
  components: {
    TaskCreate,
  },
  methods: {
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
    clickDelete(itemDelete) {
      for (let i = 0; i < this.list.length; i++) {
        if (itemDelete.id === this.list[i].id) {
          this.list.splice(i, 1);
        }
      }
    },
    clickEdit(itemEdit) {
      console.log(itemEdit);
      this.taskEdit = itemEdit;
    },
  },
  data() {
    return {
      search: "",
      // checked: false,
      taskEdit: {},
      list: [
        {
          id: 1,
          name: "Learn Vue JS",
          status: "Not started",
          deadline: "1-1-2022",
          priority: "Critical",
          completed: true,
        },
        {
          id: 2,
          name: "Watch netflix",
          status: "Pending",
          deadline: "1-2-2022",
          priority: "High",
          completed: true,
        },
        {
          id: 3,
          name: "Play soccer",
          status: "In progress",
          deadline: "1-3-2022",
          priority: "Medium",
          completed: true,
        },
        {
          id: 4,
          name: "Learn guitar",
          status: "In progress",
          deadline: "1-4-2022",
          priority: "Low",
          completed: true,
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
}
.text-success {
  color: #04aa6d;
}
.text-warning {
  color: orange;
}
</style>
