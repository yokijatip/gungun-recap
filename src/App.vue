<script setup>
import { ref } from 'vue'
import TemplateSelection from './components/TemplateSelection.vue'
import ACReportGenerator from './components/ACReportGenerator.vue'

const currentView = ref('template-selection')
const selectedTemplate = ref(null)

const handleTemplateSelect = (templateType) => {
  selectedTemplate.value = templateType
  currentView.value = 'report-generator'
}

const handleBack = () => {
  currentView.value = 'template-selection'
  selectedTemplate.value = null
}
</script>

<template>
  <div id="app">
    <TemplateSelection
        v-if="currentView === 'template-selection'"
        @select-template="handleTemplateSelect"
    />
    <ACReportGenerator
        v-else-if="currentView === 'report-generator'"
        :template="selectedTemplate"
        @back="handleBack"
    />
  </div>
</template>

<style>
#app {
  min-height: 100vh;
}
</style>
