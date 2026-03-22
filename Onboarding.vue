<template>
  <div class="onboarding gradient-bg" :class="{ visible: isVisible }">
    <div class="onboarding-content" v-show="page === 1">
      <div class="text-block">
        <div
          v-for="(line, i) in page1Lines"
          :key="i"
          class="text-line"
          :style="{ animationDelay: `${i * 0.6}s` }"
        >
          {{ line }}
        </div>
      </div>
      <div class="input-section">
        <label
          class="input-label"
          :style="{ animationDelay: `${page1Lines.length * 0.6}s` }"
        >
          在开始之前，请告诉我您的身份（职业），我将为你量身定制知识分类：
        </label>
        <input
          v-model="profession"
          type="text"
          placeholder="例如：程序员、设计师、学生..."
          class="profession-input"
        />
        <button class="next-btn" :disabled="!profession.trim()" @click="goToPage2">
          下一步
        </button>
      </div>
    </div>
    <div class="onboarding-content page2" v-show="page === 2">
      <div class="text-block" v-if="!loading">
        <div
          class="text-line"
          :style="{ animationDelay: '0s' }"
        >
          已定制您的专属知识库，准备好开启你的第二大脑了吗？
        </div>
      </div>
      <div class="loading-animation" v-if="loading">
        <div class="loader"></div>
        <span>正在为您定制知识库...</span>
      </div>
      <div class="done-content" v-else>
        <button class="start-btn" @click="finish">开始使用</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const emit = defineEmits(['complete'])

const page = ref(1)
const profession = ref('')
const loading = ref(true)
const isVisible = ref(false)

const page1Lines = [
  'Hi~ 我是 Kato。看到那些被收藏夹吃灰的链接了吗？那是知识在哭泣。',
  '把它们丢给我吧。不管是网页、文档还是图片，我来负责记忆，你负责思考。'
]

const goToPage2 = () => {
  if (!profession.value.trim()) return
  page.value = 2
  loading.value = true
  setTimeout(() => {
    loading.value = false
  }, 1500)
}

const finish = () => {
  emit('complete')
}

onMounted(() => {
  setTimeout(() => { isVisible.value = true }, 50)
})
</script>

<style scoped>
.onboarding {
  position: fixed;
  inset: 0;
  z-index: 1000;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.5s ease;
}

.onboarding.visible {
  opacity: 1;
}

.onboarding-content {
  width: 66.666vw;
  min-width: 280px;
  max-width: 800px;
  padding: 48px;
}

.text-block {
  margin-bottom: 48px;
}

.text-line {
  font-family: 'Noto Serif SC', 'SimSun', 'STSong', serif;
  font-weight: 700;
  font-size: 24px;
  line-height: 2.2;
  color: var(--color-gray-800);
  opacity: 0;
  animation: fadeInLine 1s ease forwards;
}

@keyframes fadeInLine {
  to {
    opacity: 1;
  }
}

.input-section {
  margin-top: 40px;
}

.input-label {
  display: block;
  font-family: 'Noto Serif SC', 'SimSun', 'STSong', serif;
  font-weight: 700;
  font-size: 22px;
  color: var(--color-gray-800);
  margin-bottom: 16px;
  line-height: 1.6;
  opacity: 0;
  animation: fadeInLine 1s ease forwards;
}

.profession-input {
  width: 100%;
  padding: 16px 20px;
  border: 1px solid var(--color-gray-200);
  border-radius: var(--radius);
  font-size: 16px;
  margin-bottom: 24px;
  font-family: inherit;
}

.profession-input:focus {
  outline: none;
  border-color: var(--color-green);
}

.next-btn {
  padding: 14px 36px;
  background: var(--color-green);
  color: var(--color-white);
  border: none;
  border-radius: 24px;
  font-size: 16px;
  font-weight: 500;
  cursor: pointer;
  font-family: inherit;
}

.next-btn:disabled {
  background: var(--color-gray-400);
  cursor: not-allowed;
}

.next-btn:not(:disabled):hover {
  background: #389e0d;
}

.page2 {
  text-align: center;
}

.page2 .text-block {
  margin-bottom: 32px;
}

.page2 .text-line {
  font-size: 24px;
}

.loading-animation {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 24px;
}

.loader {
  width: 48px;
  height: 48px;
  border: 3px solid var(--color-gray-200);
  border-top-color: var(--color-green);
  border-radius: 50%;
  animation: spin 0.8s linear infinite;
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

.loading-animation span {
  font-size: 15px;
  color: var(--color-gray-600);
}

.done-content {
  animation: fadeInLine 0.5s ease;
}

.start-btn {
  padding: 16px 56px;
  background: var(--color-green);
  color: var(--color-white);
  border: none;
  border-radius: 24px;
  font-size: 17px;
  font-weight: 500;
  cursor: pointer;
  font-family: inherit;
  transition: background 0.2s;
}

.start-btn:hover {
  background: #389e0d;
}
</style>
