<template>
  <section>
    <h3>Todos <button @click="addTodoHandler()">New</button></h3>
    <TodoForm
      v-if="currentTodo"
      :todo="currentTodo"
      @onAddOrUpdate="onUpdateTodoHandler"
    />
    <br />
    <table width="100%">
      <thead>
        <tr>
          <th>Id</th>
          <th>Name</th>
          <th>description</th>
          <th>Type</th>
          <th>Confidential</th>
          <th>Remind</th>
          <th>Date</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr :key="todo.id" v-for="todo in todos">
          <td>{{ todo.id }}</td>
          <td>{{ todo.name }}</td>
          <td>{{ todo.description }}</td>
          <td>{{ todo.type }}</td>
          <td>{{ todo.confidential }}</td>
          <td>{{ todo.remind.toString() }}</td>
          <td>{{ todo.date }}</td>
          <td>
            <button type="button" @click="selectTodoHandler(todo.id)">
              Edit
            </button>
            <button type="button" @click="deleteTodoHandler(todo.id)">
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </section>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';
import {
  addTodo,
  deleteTodo,
  getTodo,
  getTodos,
  Todo,
  updateTodo
} from './todos';
import TodoForm from './TodoForm.vue';

@Component({
  components: {
    TodoForm
  }
})
export default class Todos extends Vue {
  currentTodo: Partial<Todo> | null = null;
  todos: Todo[] = getTodos();

  addTodoHandler() {
    this.currentTodo = {
      confidential: 'No',
      remind: false
    };
  }

  selectTodoHandler(id: number) {
    this.currentTodo = getTodo(id);
  }

  deleteTodoHandler(id: number) {
    deleteTodo(id);
    this.todos = getTodos();
  }

  onUpdateTodoHandler(todo: Partial<Todo>) {
    if (!todo.id) {
      addTodo(todo);
    } else {
      updateTodo(todo as Todo);
    }
    this.currentTodo = null;
  }
}
</script>
