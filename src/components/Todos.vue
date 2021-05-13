<template>
  <section>
    <h3>Todos <button @click="addTodoHandler()">New</button></h3>
    <TodoView
      v-if="currentTodo && currentEvent === 'view'"
      :todo="currentTodo"
      @onClose="() => (currentTodo = null)"
    />
    <TodoForm
      v-if="currentTodo && currentEvent === 'edit'"
      :todo="currentTodo"
      @onAddOrUpdate="onUpdateTodoHandler"
    />
    <br />
    <table width="100%">
      <thead>
        <tr>
          <th align="left">Id</th>
          <th align="left">Name</th>
          <th align="left">description</th>
          <th align="left">Type</th>
          <th align="left">Confidential</th>
          <th align="left">Remind</th>
          <th align="left">Date</th>
          <th align="left">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="todo in todos" :key="todo.id">
          <td>{{ todo.id }}</td>
          <td>{{ todo.name }}</td>
          <td>{{ todo.description }}</td>
          <td>{{ todo.type }}</td>
          <td>{{ todo.confidential }}</td>
          <td>{{ todo.remind.toString() }}</td>
          <td>{{ todo.date }}</td>
          <td>
            <button type="button" @click="selectTodoHandler(todo.id, 'view')">
              View
            </button>
            &nbsp;
            <button type="button" @click="selectTodoHandler(todo.id, 'edit')">
              Edit
            </button>
            &nbsp;
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
import TodoView from './TodoView.vue';
import TodoForm from './TodoForm.vue';

@Component({
  components: {
    TodoView,
    TodoForm
  }
})
export default class Todos extends Vue {
  currentTodo: Partial<Todo> | null = null;
  currentEvent: string | null = null;
  todos: Todo[] = getTodos();

  addTodoHandler() {
    this.currentEvent = 'edit';
    this.currentTodo = {
      confidential: 'No',
      remind: false
    };
  }

  selectTodoHandler(id: number, currentEvent: string) {
    this.currentEvent = currentEvent;
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
