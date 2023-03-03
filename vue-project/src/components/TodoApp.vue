<template>
  <div class="container">
    <div class="header">
      <h1 class="title">
        {{ titlehead }}
        <i class="fa-regular fa-sun"></i>
      </h1>
    </div>
    <form @submit.prevent="addTodo">
      <input
        class="input"
        v-model="newTodo"
        type="text"
        name="newTodo"
        placeholder="Create a new todo..."
      />
    </form>
    <ul>
      <li v-for="todo in todos">
        <input type="checkbox" v-model="todo.done" />

        <div class="delete">
          <span :class="{ done: todo.done }">{{ todo.title }}</span>
          <div class="btn">
            <button @click="editTask(todo)" class="submit">
              <i class="fa-solid fa-pen"></i>
            </button>
            <button @click="deleteTodo(todo)" type="submit" class="submit">
              <i class="fa-solid fa-trash"></i>
            </button>
          </div>
        </div>
        <hr />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "TodoApp",
  data() {
    return {
      titlehead: "Todo",
      newTodo: "",
      todos: [],
      editedTask: null,
    };
  },
  methods: {
    addTodo() {
      if (this.editedTask === null) {
        this.todos.push({
          title: this.newTodo,
          done: false,
        });
      } else {
        this.todos[this.editedTask].title = this.newTodo;
        this.editedTask = null;
      }
      this.newTodo = "";
    },
    deleteTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
    allDone() {
      this.todos.forEach((todo) => {
        todo.done = true;
      });
    },
    editTask(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.newTodo = this.todos[todoIndex].title;
      this.editedTask = todoIndex;
    },
  },
};
</script>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
