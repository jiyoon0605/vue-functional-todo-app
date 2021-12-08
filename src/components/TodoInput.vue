<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="fas fa-plus addBtn"></i>
    </span>
  </div>
</template>
<script>
export default {
  data: () => {
    return {
      newTodoItem: ""
    }
  },
  methods: {
    addTodo: function () {
      if (this.newTodoItem === '') {
        return;
      }
     const todoItem = this.newTodoItem;
      this.clearInput();
      this.$emit('addTodo', todoItem);

    },
    clearInput: function () {
      this.newTodoItem = "";
    }
  }
}
</script>
<style scoped>
input:focus {
  outline: none;
}

.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
  display: flex;
}

input {
  border-style: none;
  font-size: 0.9rem;
  box-sizing: border-box;
  padding: 0 10px;
  flex: fit-content;
}

.addContainer {
  float: right;
  background: linear-gradient(to right, #6478FB, #8763FB);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}

.addBtn {
  color: white;
  vertical-align: middle;
}

</style>