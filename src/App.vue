<template>
  <div id="app">
    <MonacoEditor
      class="editor"
      v-model="code"
      language="jinja2"
      theme="vs-dark"
      :options="options"
      @editorDidMount="editorDidMount"
      ref="editor"
    />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import MonacoEditor from "vue-monaco";

import { conf, language } from "./jinja2";

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

  editorDidMount(editor: any) {
    const monaco = (this.$refs.editor as any).monaco;

    monaco.languages.register({ id: "jinja2" });
    monaco.languages.setLanguageConfiguration("jinja2", conf);
    monaco.languages.setMonarchTokensProvider("jinja2", language);

    monaco.languages.registerCompletionItemProvider("jinja2", {
      provideCompletionItems: () => {
        const suggestions = [
          {
            label: "simpleText",
            kind: monaco.languages.CompletionItemKind.Text,
            insertText: "simpleText"
          }
        ];
        return { suggestions };
      }
    });
  }
}
</script>

<style lang="sass">
.editor
  width: 600px
  height: 800px
</style>
