<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "my-Button",
};
</script>

<style scoped>
.btn {
  padding: 10px 15px;
  background: none;
  color: rgb(0, 0, 0);
  border: 1px solid teal;
  background-color: rgba(8, 144, 255, 0.616);
  border-radius: 5px;
  cursor: pointer;
  transition: all 0.5s ease;
}
.btn:hover {
  background-color: rgb(8, 144, 255);
}
</style>
