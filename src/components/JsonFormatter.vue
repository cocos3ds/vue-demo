<template>
    <div class="common-layout">
        <el-container>
            <el-header>JSON 编辑器</el-header>
            <el-container>
                <el-aside width="45%">
                    <div>
                        <MonacoEditor/>
                    </div>
                </el-aside>
                <el-main>
                    <div>
                        <vue-json-pretty :data="json_obj" :showLineNumber="true" :editable="true"/>
                    </div>
                </el-main>
            </el-container>
        </el-container>
    </div>
  </template>
  
  <script setup lang="ts">
    import {ref,computed} from 'vue';
    import VueJsonPretty from 'vue-json-pretty';
    import MonacoEditor from './MonacoEditor.vue'
    import 'vue-json-pretty/lib/styles.css';
    let json = ref('')

  const json_obj = computed(()=>{
    if(json.value != ''){
        try{
            return JSON.parse(json.value)
        }catch(e){
           return {}     
        }
    }
    return {}
    
  })
 
  </script>

<style scoped>
    .el-main{
        overflow: scroll;
        height:873px;
        border:1px solid #626467;
    }
</style>