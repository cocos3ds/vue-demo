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
    value: '{\n\
    "widget": {\n\
      "debug": "on",\n\
      "window": {\n\
          "title": "Sample Konfabulator Widget",\n\
          "name": "main_window",\n\
          "width": 500,\n\
          "height": 500\n\
      },\n\
      "image": { \n\
          "src": "Images/Sun.png",\n\
          "name": "sun1",\n\
          "hOffset": 250,\n\
          "vOffset": 250,\n\
          "alignment": "center"\n\
      },\n\
      "text": {\n\
          "data": "Click Here",\n\
          "size": 36,\n\
          "style": "bold",\n\
          "name": "text1",\n\
          "hOffset": 250,\n\
          "vOffset": 100,\n\
          "alignment": "center",\n\
          "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"\n\
      }\n\
  }\n\
}',
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
