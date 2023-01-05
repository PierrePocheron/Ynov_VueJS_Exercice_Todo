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
        />
      </header>

      <section class="main">
        <input id="toggle-all" type="checkbox" class="toggle-all" />
        <label for="toggle-all">Mark all as complete</label>
        <ul v-for="task in taskList" :key="task.id" class="todo-list">
          <li class="todo">
            <div class="view">
              <!-- If status = checked add property checked -->
              <input type="checkbox" class="toggle" checked />
              <label>{{ task.name }}</label>
              <button class="destroy"></button>
            </div>
            <input type="text" class="edit" value="{{ task.name }}" />
          </li>
        </ul>
      </section>

      <footer class="footer">
        <span class="todo-count"> <strong>1</strong> item left </span>
        <ul class="filters">
          <li><a href="#/all" class="selected">All</a></li>
          <li><a href="#/active">Active</a></li>
          <li><a href="#/completed">Completed</a></li>
        </ul>
        <button class="clear-completed">Clear completed</button>
      </footer>
    </section>
    <footer class="info">
      <p>Double-click to edit a todo</p>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      taskList: [
        { id: 1, name: "Task 1", status: true },
        { id: 2, name: "Task 2", status: true },
        { id: 3, name: "Task 3", status: false },
      ],
    };
  },

  setup() {},
};
</script>
