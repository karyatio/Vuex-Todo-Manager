<template>
  <div>
    <h3>Todos</h3>

    <div class="legend">
      <span>Double click to mark as complete</span>
      <span>
        <span class="incomplete-box">= Incomplete</span>
      </span>
      <span>
        <span class="complete-box">= Complete</span>
      </span>
    </div>

    <div class="todos">
      <div
        v-for="todo in allTodos"
        @dblclick="onDblClick(todo)"
        v-bind:key="todo.id"
        class="todo"
        v-bind:class="{'is-complete' : todo.completed}"
      >
        {{todo.title}}
        <i @click="deleteTodo(todo.id)" class="fas fa-trash-alt"></i>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";

export default {
  name: "Todos",
  methods: {
    ...mapActions(["fetchTodos", "deleteTodo", "updateTodo"]),
    onDblClick(todo) {
      const upTodo = {
        id: todo.id,
        title: todo.title,
        completed: !todo.completed
      };

      this.updateTodo(upTodo);
    }
  },
  computed: mapGetters(["allTodos"]),
  created() {
    this.fetchTodos();
  }
};
</script>

<style scoped>
.legend {
  display: flex;
  justify-content: space-around;
  margin-bottom: 1rem;
}

.complete-box {
  display: inline-block;
  width: 10px;
  height: 10px;
  background: #35495e;
}

.incomplete-box {
  display: inline-block;
  width: 10px;
  height: 10px;
  background: #41b883;
}

.is-complete {
  background-color: #35495e !important;
  color: #fff;
}

.todos {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;
}

.todo {
  border: 1px solid #ccc;
  background: #41b883;
  padding: 1rem;
  text-align: center;
  position: relative;
  cursor: pointer;
}

@media (max-width: 500px) {
  .todos {
    grid-template-columns: 1fr;
  }
}

i {
  position: absolute;
  bottom: 10px;
  right: 10px;
  color: #fff;
  cursor: pointer;
}
</style>
