<template>
        <el-container>
                <el-aside width="45%">
                    <div>
                        <MonacoEditor @response="(payload) => { json = payload }" />
                    </div>
                </el-aside>
                <el-main class="json-preview-area">
                    <div>
                        <vue-json-pretty :data="json_obj" :showLineNumber="true" :editable="true" />
                    </div>
                </el-main>
            </el-container>
</template>

<script setup lang="ts">
import VueJsonPretty from 'vue-json-pretty';
import MonacoEditor from './MonacoEditor.vue'
import { ref, computed } from 'vue';
import JSConfetti from 'js-confetti'
import 'vue-json-pretty/lib/styles.css';
let json = ref('')

const confetti = new JSConfetti()
let count = 0;
const json_obj = computed(() => {
    if (json.value != '') {
        try {
            let result =  JSON.parse(json.value)
            if(count == 1){
                confetti.addConfetti();
            }
            if(count >= 1){
                // @ts-ignore
                gtag('event', 'inputjson', {
                                'app_name': 'jsonv2',
                                'screen_name': 'home'
                                });
            }
            count++;
            return result;
        } catch (e) {
            return {}
        }
    }
    return {}

})
</script>