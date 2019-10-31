<template>
  <div id="app">
    <MonacoEditor class="editor" v-model="code" language="json" theme="vs-dark" :options="options" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import MonacoEditor from "vue-monaco";

@Component({
  components: {
    MonacoEditor
  }
})
export default class App extends Vue {
  code = "";
  options = {
    minimap: {
      enabled: false
    }
  };
}
</script>

<style lang="sass">
.editor
  width: 600px
  height: 800px
</style>
