<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="fas fa-plus addBtn"></i>
    </span>
    <Modal v-if="showModal">
      <h3 slot="header">Warning!<i class="fas fa-times closeModalBtn" @click="closeModal"/></h3>
      <div slot="body">내용을 입력해 주세요</div>
    </Modal>
  </div>
</template>
<script>
import Modal from "@/components/common/Modal";

export default {
  data: () => {
    return {
      newTodoItem: "",
      showModal: false,
    }
  },
  methods: {
    addTodo: function () {
      if (this.newTodoItem === '') {
        this.showModal = true;
        return;
      }
      this.$emit('addTodo', this.newTodoItem);
      this.clearInput();
    },
    clearInput: function () {
      this.newTodoItem = "";
    },
    closeModal: function () {
      this.showModal = false;
    }
  },
  components: {
    Modal
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

h3 {
  color: #42b983;
}

.closeModalBtn {
  color: #42b983;
}
</style>