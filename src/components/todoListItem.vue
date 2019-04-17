<template lang="pug">
  .todo-item(:class="{checked: todo.checked}")
    label.label
      .input-block
        input.input(
          type="checkbox"
          @change="checkTodo"
          :checked="todo.checked"
        )
        .title {{todo.name}}
      .buttons
        button.btn-remove(
          type="button"
            @click="removeTodo"
          ) x
</template>

<script>
export default {
  props: {
    todo: {}
  },
  methods: {
    removeTodo() {
      this.$emit('removeTodo', this.todo.id)
    },
    checkTodo(e) {
      console.log(e.target);
      const todoItem = {        //???
        ...this.todo,           
        checked: e.target.checked
      }
      
      this.$emit('checkTodo', todoItem);
    }
  }
}
</script>


<style lang="scss" scoped>
.todo-item {
  display: flex;
  align-items: center;

  &:hover {
    .remove {
      visibility: visible;
    }

    .view {
      visibility: visible;
    }
  }
}

.view {
  visibility: hidden;
  cursor: pointer;
}

.checked .title {
  text-decoration: line-through;
}

.label {
  display: flex;
  align-items: center;
  flex: 1;
}

.input-block {
  display: flex;
  align-items: center;
  justify-content: start;
  flex: 1;
}

.title {
  padding: 15px 0 15px 15px;
  display: block;
  line-height: 1.2;
}

.button {
  width: 40px;
}

.remove {
  background: transparent;
  border: none;
  color: firebrick;
  cursor: pointer;
  font-size: 20px;
  visibility: hidden;
}
</style>