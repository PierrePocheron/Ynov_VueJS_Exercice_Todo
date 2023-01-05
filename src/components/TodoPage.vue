<template>
  <div>
    <section class="todoapp">
      <header class="header">
        <h1>todos</h1>
        <input
          autofocus="autofocus"
          autocomplete="off"
          placeholder="What needs to be done?"
          class="new-todo"
          v-model="nameTask"
          @keyup.enter="addTask()"
        />
      </header>

      <section class="main">
        <input
          id="toggle-all"
          type="checkbox"
          class="toggle-all"
          v-model="inputToggleAll"
          @change="updateAllTaskStatus()"
        />
        <label for="toggle-all">Mark all as complete</label>
        <ul v-for="task in taskList" :key="task.id" class="todo-list">
          <li class="todo">
            <div class="view">
              <!-- If status = checked add property checked -->
              <input
                type="checkbox"
                class="toggle"
                :checked="task.status"
                @click="updateTaskStatus(task.id, !task.status)"
              />
              <label>{{ task.name }}</label>
              <button class="destroy" @click="removeTask(task.id)"></button>
            </div>
            <input type="text" class="edit" value="{{ task.name }}" />
          </li>
        </ul>
      </section>

      <footer class="footer">
        <span class="todo-count">
          <strong> {{ counterTaskLeft }} </strong> item left
        </span>
        <ul class="filters">
          <li><a href="#/all" class="selected">All</a></li>
          <li><a href="#/active">Active</a></li>
          <li><a href="#/completed">Completed</a></li>
        </ul>
        <button class="clear-completed" @click="removeTaskCompleted()">
          Clear completed
        </button>
      </footer>
    </section>
    <footer class="info">
      <p>Double-click to edit a todo</p>
    </footer>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  data() {
    return {
      taskList: [
        { id: 1, name: "Task 1", status: true },
        { id: 2, name: "Task 2", status: true },
        { id: 3, name: "Task 3", status: false },
      ],
      nextId: 4,
      nameTask: "",
      inputToggleAll: false,
    };
  },

  methods: {
    addTask() {
      this.taskList.push({
        id: this.nextId,
        name: this.nameTask,
        status: false,
      });
      this.nextId++;
      this.nameTask = "";
    },

    removeTask(id) {
      this.taskList = this.taskList.filter((task) => task.id !== id);
    },

    removeTaskCompleted() {
      this.taskList = this.taskList.filter((task) => !task.status);
    },

    updateTaskStatus(id, status) {
      this.taskList = this.taskList.map((task) => {
        if (task.id === id) {
          task.status = status;
        }
        return task;
      });
    },

    updateAllTaskStatus() {
      this.taskList.forEach((task) => {
        task.status = this.inputToggleAll;
      });
    },
  },

  computed: {
    counterTaskLeft: function () {
      var tasksLeft = this.taskList.filter((task) => !task.status);
      return tasksLeft.length;
    },
  },

  setup() {},
};
</script>
