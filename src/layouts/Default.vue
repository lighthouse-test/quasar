<template>
  <section>
    <header>
      <h1>Quasar Demo</h1>
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
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';

@Component({
  components: {}
})
export default class Default extends Vue {}
</script>
