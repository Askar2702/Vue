<template>
  <div class="container">
    <h2 class="text-title">ToDo</h2>
    <my-Input v-model="searchQuery" placeholder="Поиск...." />

    <div class="app__btns">
      <my-Button @click="showDialog"> Создать задачу </my-Button>
      <MySelect v-model="selectedSort" :options="sortOptions" />
    </div>
    <MyDialog v-model:show="dialogVisible">
      <input-form
        @create="createTodo"
        v-bind:titleTodo="this.currentTodo.title"
        v-bind:bodyTodo="this.currentTodo.body"
      />
    </MyDialog>
    <TodoList
      :todos="sortedAndSearchedTodos"
      @remove="removeTodo"
      @rename="renameTodo"
      @changeStatus="changeStatus"
    />
  </div>
</template>

<script>
import InputForm from "./InputForm.vue";
import TodoList from "./TodoList.vue";
import MyDialog from "./UI/MyDialog.vue";
import MySelect from "./UI/MySelect.vue";

export default {
  components: {
    InputForm,
    TodoList,
    MyDialog,
    MySelect,
  },

  data() {
    return {
      titlePage: "",
      isUpdateTodo: false,
      currentTodo: {
        type: Object,
      },
      searchQuery: "",
      dialogVisible: false,
      todos: [],
      selectedSort:
        localStorage.getItem("selectedSort") === "null"
          ? "All"
          : localStorage.getItem("selectedSort"),
      sortOptions: [
        { value: "complected", name: "Завершены" },
        { value: "open", name: "Открыты" },
        { value: "All", name: "Все" },
      ],
    };
  },

  methods: {
    showDialog() {
      if (!this.isUpdateTodo) {
        this.currentTodo = {
          id: null,
          title: "",
          body: "",
        };
      }
      this.dialogVisible = true;
    },
    createTodo(todo) {
      if (todo.title === "" || todo.body === "") return;
      if (!this.isUpdateTodo) {
        this.todos.push(todo);
        document.title = todo.titlePage;
        console.log(todo.titlePage);
        console.log(document.title);
        this.dialogVisible = false;
        // вторая часть кода для переименования
      } else {
        this.currentTodo.title = todo.title;
        this.currentTodo.body = todo.body;
        document.title = todo.titlePage;
        this.isUpdateTodo = false;
        this.dialogVisible = false;
      }

      this.saveData();
    },

    saveData() {
      localStorage.setItem("Todo", JSON.stringify(this.todos));
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((p) => p.id !== todo.id);
      this.saveData();
    },

    renameTodo(todo) {
      this.currentTodo = todo;
      this.isUpdateTodo = true;
      this.showDialog();
    },

    changeStatus(post) {
      post.status = post.status === "open" ? "complected" : "open";
      this.saveData();
    },
  },

  mounted() {
    const todo = localStorage.getItem("Todo");

    if (todo !== null) this.todos = JSON.parse(todo);
    this.selectedSort = localStorage.getItem("selectedSort");
  },

  computed: {
    sortedTodos() {
      localStorage.setItem("selectedSort", this.selectedSort);

      if (this.selectedSort === "All") return [...this.todos];
      else {
        return [...this.todos].filter(
          (todo) => todo.status === this.selectedSort
        );
      }
    },
    sortedAndSearchedTodos() {
      return this.sortedTodos.filter((post) =>
        post.title.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },

  watch: {
    dialogVisible() {
      if (!this.dialogVisible) {
        this.currentTodo = {
          id: null,
          title: "",
          body: "",
        };
      }
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  background-color: beige;
}
.container {
  margin: 0;
}
.app__btns {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}
</style>
