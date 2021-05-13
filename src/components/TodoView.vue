<template>
  <section>
    <h4>Todo</h4>
    <table>
      <tbody>
        <tr>
          <th align="left">Name</th>
          <td>
            {{ todo.name }}
          </td>
        </tr>
        <tr>
          <th align="left">Description</th>
          <td>
            {{ todo.description }}
          </td>
        </tr>
        <tr>
          <th align="left">Type</th>
          <td>{{ todo.type }}</td>
        </tr>
        <tr>
          <th align="left">Confidential</th>
          <td>
            {{ todo.confidential }}
          </td>
        </tr>
        <tr>
          <th align="left">Remind</th>
          <td>{{ todo.remind }}</td>
        </tr>
        <tr>
          <th align="left">Date</th>
          <td>{{ todo.date }}</td>
        </tr>
        <tr>
          <th colspan="2" align="right">
            <button type="button" @click="closeTodoHandler">Close</button>
          </th>
        </tr>
      </tbody>
    </table>
  </section>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator';
import { Todo } from './todos';

@Component
export default class TodoForm extends Vue {
  @Prop({ type: Object, required: true }) readonly todo!: Partial<Todo>;

  closeTodoHandler = () => {
    this.$emit('onClose');
  };
}
</script>
