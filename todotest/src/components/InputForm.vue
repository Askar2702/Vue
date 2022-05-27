<template>
  <form @submit.prevent>
    <h4>{{ formTitle }}</h4>
    <my-Input v-model="todo.title" type="text" placeholder="Название" />
    <my-Input v-model="todo.body" type="text" placeholder="Описание" />
    <my-Input
      v-model="todo.titlePage"
      type="text"
      placeholder="Изменить заголовок странички"
    />

    <my-Button
      style="align-self: flex-end; margin-top: 15px"
      @click="createTodo"
    >
      {{ formBtn }}
    </my-Button>
  </form>
</template>

<script>
export default {
  props: {
    titleTodo: {
      type: String,
      default: "",
    },
    bodyTodo: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      formTitle: "",
      formBtn: "",
      todo: {
        title: "",
        body: "",
        status: "open",
        titlePage: "",
      },
    };
  },
  methods: {
    createTodo() {
      this.todo.id = Date.now();
      this.$emit("create", this.todo);
      this.todo = {
        title: "",
        body: "",
      };
    },
  },
  mounted() {
    this.todo.title = this.titleTodo;
    this.todo.body = this.bodyTodo;

    if (this.titleTodo === "") {
      this.formTitle = "Создание карточки";
      this.formBtn = "Создать";
    } else {
      this.formTitle = "Обновить карточки";
      this.formBtn = "Обновить";
    }
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}
</style>
