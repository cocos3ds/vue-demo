<template>
    <div class="common-layout">
        <el-container>
            <el-header height="107px">
                <el-container>
                    <el-aside width="200px" class="logo-area">JSON Editor</el-aside>
                    <el-main>
                        <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal">
                            <el-menu-item index="1" @click="showHomeView">Home</el-menu-item>
                            <el-menu-item index="2" @click="showComeSoonView">Introduce json</el-menu-item>
                            <el-menu-item index="3" @click="showComeSoonView">Text Diff</el-menu-item>
                            <el-menu-item index="4" @click="showComeSoonView">Learn to code</el-menu-item>
                        </el-menu>
                    </el-main>
                </el-container>
            </el-header>
            <component :is="currentView" />
        </el-container>
    </div>
</template>
  
<script setup lang="ts">
import { ref, computed } from "vue"
import CodeView from './CodeView.vue'
import ComeSoon from './ComeSoon.vue'

const activeIndex = ref('1')
let currentView = ref(CodeView)

function showComeSoonView() {
    currentView.value = ComeSoon
}

function showHomeView() {
    currentView.value = CodeView
}



</script>

<style scoped>
.json-preview-area {
    overflow: scroll;
    height: 873px;
    border: 1px solid #626467;
}

.logo-area {
    display: flex;
    justify-content: center;
    align-items: center;
}

#editor {
    border: 1px solid #0000003b
}
</style>