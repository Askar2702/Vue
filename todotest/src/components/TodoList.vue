<template>
  <h3>Список задач</h3>
  <div class="container">
    <transition-group name="user-list">
      <todo-item
        v-for="todo in todos"
        :todo="todo"
        :key="todo.id"
        @rename="$emit('rename', todo)"
        @remove="$emit('remove', todo)"
        @changeStatus="$emit('changeStatus', todo)"
      />
    </transition-group>
  </div>
</template>

<script>
import TodoItem from "@/components/TodoItem.vue";
export default {
  components: { TodoItem },
  props: {
    todos: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
/* для анимаций эти классы */
.container {
  display: grid;
  /* grid-template-columns: 1fr 1fr 1fr; */
}
.user-list-item {
  display: inline-flex;
  margin-right: 10px;
}

.user-list-enter-active,
.user-list-leave-active {
  transition: all 0.4s ease;
}
.user-list-enter-from,
.user-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}
.user-list-move {
  transition: transform 0.4s ease;
}

@media (min-width: 320px) {
  .container {
    grid-template-columns: 1fr;
  }
}

@media (min-width: 960px) {
  .container {
    grid-template-columns: 1fr 1fr 1fr;
  }
}
</style>
