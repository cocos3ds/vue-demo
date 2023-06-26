<template>
    <div class="common-layout">
        <el-container>
            <el-header height="107px">
                <el-container>
      <el-aside width="200px" class="logo-area">JSON Editor</el-aside>
      <el-main>
    <el-menu
    :default-active="activeIndex"
    class="el-menu-demo"
    mode="horizontal"
  >
    <el-menu-item index="1">About</el-menu-item>
    <el-menu-item index="3">Introduce json</el-menu-item>
  </el-menu></el-main>
    </el-container>
  
</el-header>

            <el-container>
                <el-aside width="45%">
                    <div>
                        <MonacoEditor @response="(payload)=>{json = payload}"/>
                    </div>
                </el-aside>
                <el-main class="json-preview-area">
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
    const activeIndex = ref('1')

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
    .json-preview-area{
        overflow: scroll;
        height:873px;
        border:1px solid #626467;
    }
    .logo-area{
        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>