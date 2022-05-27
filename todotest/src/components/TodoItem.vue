<template>
  <div class="todo">
    <div class="container">
      <div>
        <div><strong>Название:</strong> {{ todo.title }}</div>
        <div><strong>Описание:</strong> {{ todo.body }}</div>
      </div>
      <div class="todo__btns">
        <button class="btn-done" @click="changeStatus">
          <img
            v-if="isComplected === true"
            src="https://cdn-icons.flaticon.com/png/512/2794/premium/2794680.png?token=exp=1650364323~hmac=99d037d3522cab82dc21f72f41d7f1a2"
            alt=""
          />
          <img
            v-else
            src="https://cdn-icons.flaticon.com/png/512/2794/premium/2794649.png?token=exp=1650364796~hmac=e74de870bebd212fe92de88dc0cec012"
            alt=""
          />
        </button>
        <my-Button @click="$emit('rename', todo)"> Переименовать </my-Button>
        <my-Button @click="$emit('remove', todo)"> Удалить </my-Button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isComplected: false,
    };
  },
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },

  methods: {
    changeStatus() {
      this.$emit("changeStatus", this.todo);
      this.isComplected = !this.isComplected;
    },
  },
  mounted() {
    if (this.todo.status === "complected") {
      this.isComplected = true;
    } else this.isComplected = false;
  },
};
</script>

<style scoped>
.todo {
  display: flex;
  justify-content: center;
  align-items: center;
}
.container {
  width: 300px;
  padding: 15px;
  background-color: rgba(253, 220, 31, 0.445);
  border: 2px solid rgba(253, 220, 31, 0.445);
  border-radius: 5px;
  margin: 15px 0;
  display: block;
  align-items: center;
  justify-content: space-between;
  box-shadow: 10px 5px 5px rgb(145, 233, 255);
}
.todo__btns {
  margin-top: 10px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.todo__btns button {
  width: 100%;
  margin: 5px 0;
}

.btn-done {
  background: none;
  outline: none;
  border: none;
}

.btn-done img:hover {
  cursor: pointer;
  transform: scale(1.1);
}
.btn-done,
img {
  width: 100px;
  height: 100px;
  background-size: cover;
  transition: all 0.2s ease-in-out;
}
</style>
