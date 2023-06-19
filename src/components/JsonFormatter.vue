<template>
    <div class="common-layout">
        <el-container>
                <el-header>JSON 编辑器</el-header>
            <el-container>
                <el-aside width="600px">
                    <div>
                        <el-input
                            v-model="json"
                            :rows="100"
                            type="textarea"
                            placeholder="Please input"
                        />
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
    import {ref,computed} from 'vue'
    import VueJsonPretty from 'vue-json-pretty';
    import 'vue-json-pretty/lib/styles.css';
    let json = ref('')

  const json_obj = computed(()=>{
    if(json.value != ''){
        return JSON.parse(json.value)
    }
    return {}
    
  })
 
  </script>