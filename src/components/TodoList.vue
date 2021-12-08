<template>
  <div>
    <ul>
      <li class="shadow" v-for="(todoItem ,i) of todoItems" v-bind:key="i">
        <i class="fas fa-check checkBtn " :class="{checkBtnCompleted: todoItem.completed}"
           v-on:click="toggleComplete(todoItem)"></i>
        <span :class="{textCompleted: todoItem.completed}" v-text="todoItem.item"/>
        <span v-on:click="removeTodo(todoItem.item, i)">
           <i class="fas fa-trash-alt removeBtn"></i>
        </span>
      </li>
    </ul>

  </div>
</template>
<script>
export default {
  props: ['todoItems'],
  methods: {
    removeTodo: function (item, index) {
      this.$emit('removeTodo', item, index);
    },
    toggleComplete: function (item) {
      this.$emit('toggleComplete', item);
    }
  },
}
</script>
<style scoped>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}

li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 54px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
  justify-content: space-between;
}

.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}

.checkBtnCompleted {
  color: #b3adad;
}

.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}

.removeBtn {
  margin-right: auto;
  color: #de4343;
}

</style>