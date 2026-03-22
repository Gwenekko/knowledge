<template>
  <div class="app gradient-bg">
    <Onboarding v-if="showOnboarding" @complete="handleOnboardingComplete" />
    <main v-else class="main-view">
      <header class="header">
        <h1 class="logo">Kato 知识库</h1>
      </header>
      <ChatArea />
      <KnowledgeDetail v-if="selectedCategory" :category="selectedCategory" @back="selectedCategory = null" />
      <KnowledgeBase v-else @select="selectedCategory = $event" />
    </main>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Onboarding from './components/Onboarding.vue'
import ChatArea from './components/ChatArea.vue'
import KnowledgeBase from './components/KnowledgeBase.vue'
import KnowledgeDetail from './components/KnowledgeDetail.vue'

const showOnboarding = ref(true)
const selectedCategory = ref(null)

const handleOnboardingComplete = () => {
  showOnboarding.value = false
}
</script>

<style scoped>
.app {
  min-height: 100vh;
}

.main-view {
  padding-top: 32px;
  padding-bottom: 24px;
}

.header {
  text-align: center;
  margin-bottom: 32px;
}

.logo {
  font-size: 22px;
  font-weight: 600;
  color: var(--color-gray-800);
  letter-spacing: 0.5px;
}
</style>
