<script setup lang="ts">
import * as monaco from 'monaco-editor/esm/vs/editor/editor.api';

import { ref, onMounted } from 'vue'
// @ts-ignore
// import customLangMonarch from '@/custom-lang-monarch'

// monaco.languages.register({ id: 'custom' })
// monaco.languages.setMonarchTokensProvider('custom', customLangMonarch)

const emit = defineEmits(['response'])
const editor = ref()

let editor_instance:monaco.editor.IStandaloneCodeEditor;
onMounted(() => {
  editor_instance = monaco.editor.create(editor.value, {
    value: '{"please type json string":"here"}',
	  language: 'json',
    minimap:{
      enabled:false
    }
  })
  if(editor_instance){
    editor_instance.onDidChangeModelContent(()=>{
      emit('response',editor_instance.getValue())
    })
  }
  emit('response',editor_instance.getValue())
  
  
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
