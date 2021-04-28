<template>
  <section>
    <h2>Home</h2>
    <Todos />
  </section>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';
import Todos from '../components/Todos.vue';

@Component({
  components: { Todos },
  meta: {
    title: 'Lighthouse Test | Quasar',
    meta: {
      description: { name: 'description', content: 'Lighthouse Test | Quasar' }
    }
  }
})
export default class PageIndex extends Vue {}
</script>
