<template>
  <!-- <q-layout view="lHh Lpr lFf">
    <q-page-container> -->
  <section>
    <header>
      <h1>SvelteKit Demo</h1>
      <nav>
        <a href="/">Home</a>
      </nav>
    </header>
    <br />
    <router-view />
    <br />
    <footer>
      Check the lighthouse results at
      <a
        href="https://lighthouse-test.github.io"
        rel="noopener"
        target="_blank"
      >
        https://lighthouse-test.github.io
      </a>
    </footer>
  </section>
  <!-- </q-page-container>
  </q-layout> -->
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';

@Component({
  components: {}
})
export default class MainLayout extends Vue {}
</script>
