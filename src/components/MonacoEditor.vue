<script setup lang="ts">
import * as monaco from 'monaco-editor/esm/vs/editor/editor.api'
import { ref, onMounted } from 'vue'
// @ts-ignore
import customLangMonarch from '@/custom-lang-monarch'

monaco.languages.register({ id: 'custom' })
monaco.languages.setMonarchTokensProvider('custom', customLangMonarch)


const editor = ref()

onMounted(() => {
   monaco.editor.create(editor.value, {
    value: `{}`,
    language: 'custom',
  })
})
</script>

<template>
  <div id="editor" ref="editor"></div>
</template>

<style scoped>
#editor {
  width: 40vw;
  height: 90vh;
}
</style>
