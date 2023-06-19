<script setup lang="ts">
import * as monaco from 'monaco-editor/esm/vs/editor/editor.api'
import { ref, onMounted } from 'vue'
// @ts-ignore


monaco.languages.register({ id: 'custom' })


const editor = ref()

onMounted(() => {
  monaco.editor.create(editor.value, {
    value: `{}`,
    language: 'javascript',
  })
})
</script>

<template>
  <div id="editor" ref="editor"></div>
</template>

<style scoped>
#editor {
  width: 100vw;
  height: 100vh;
}
</style>
