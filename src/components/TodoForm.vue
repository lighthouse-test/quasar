<template>
  <section>
    <h4>{{ todo.id ? 'Update' : 'Add' }} Todo</h4>
    <form novalidate @submit="updateTodoHandler">
      <table>
        <tbody>
          <tr>
            <th align="left">
              <label for="name">Name</label>
            </th>
            <td>
              <input
                id="name"
                v-model="todo.name"
                type="text"
                name="name"
                required
              />
            </td>
            <td>{{ errors.name }}</td>
          </tr>
          <tr>
            <th align="left">
              <label for="description">Description</label>
            </th>
            <td>
              <textarea
                id="description"
                v-model="todo.description"
                name="description"
                required
              ></textarea>
            </td>
            <td>{{ errors.description }}</td>
          </tr>
          <tr>
            <th align="left">
              <label>Type</label>
            </th>
            <td>
              <select id="type" v-model="todo.type" name="type" required>
                <option v-for="type in types" :key="type" :value="type">
                  {{ type }}
                </option>
              </select>
            </td>
            <td>{{ errors.type }}</td>
          </tr>
          <tr>
            <th align="left">
              <label>Confidential</label>
            </th>
            <td>
              <label for="confidential1">Yes</label>
              <input
                id="confidential1"
                v-model="todo.Confidential"
                type="radio"
                name="confidential"
                value="Yes"
              />
              <label for="confidential2">No</label>
              <input
                id="confidential2"
                v-model="todo.Confidential"
                type="radio"
                name="confidential"
                value="No"
              />
            </td>
            <td></td>
          </tr>
          <tr>
            <th align="left">
              <label>Remind</label>
            </th>
            <td>
              <label for="remind">Yes</label>
              <input
                id="remind"
                v-model="todo.remind"
                type="checkbox"
                name="remind"
              />
            </td>
            <td></td>
          </tr>
          <tr>
            <th align="left">
              <label for="date">Date</label>
            </th>
            <td>
              <input
                id="date"
                v-model="todo.date"
                type="date"
                name="date"
                required
              />
            </td>
            <td>{{ errors.date }}</td>
          </tr>
          <tr>
            <th colspan="2" align="right">
              <button type="submit">{{ todo.id ? 'Update' : 'Add' }}</button>
            </th>
          </tr>
        </tbody>
      </table>
    </form>
  </section>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator';
import { Todo, TodoErrorStatus, TYPES } from './todos';

@Component
export default class TodoForm extends Vue {
  @Prop({ type: Object, required: true }) readonly todo!: Partial<Todo>;

  types: string[] = TYPES;

  errors: TodoErrorStatus = {
    status: false
  };

  // eslint-disable-next-line
  updateTodoHandler = (event: any) => {
    // eslint-disable-next-line
    event.preventDefault();
    this.errors = { status: false };
    if (!this.todo.name) {
      this.errors.name = 'Name is required.';
      this.errors.status = true;
    }
    if (!this.todo.description) {
      this.errors.description = 'Description is required.';
      this.errors.status = true;
    }
    if (!this.todo.type) {
      this.errors.type = 'Type is required.';
      this.errors.status = true;
    }
    if (!this.todo.date) {
      this.errors.date = 'Date is required.';
      this.errors.status = true;
    }
    setTimeout(() => {
      if (!this.errors.status) {
        this.$emit('onAddOrUpdate', this.todo);
      } else {
        alert('All Fields are required');
      }
    });
  };
}
</script>
