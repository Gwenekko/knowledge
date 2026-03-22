<template>
  <section class="chat-section">
    <div class="mascot-wrapper">
      <KatoMascot />
    </div>
    <div class="chat-container">
      <div class="chat-tabs">
        <button
          v-for="mode in modes"
          :key="mode.id"
          :class="['tab-btn', { active: currentMode === mode.id }]"
          @click="currentMode = mode.id"
        >
          {{ mode.label }}
        </button>
      </div>
      <div class="chat-body">
        <div class="placeholder">{{ currentPlaceholder }}</div>
        <div class="input-area">
          <input
            type="text"
            :placeholder="currentInputPlaceholder"
            readonly
            class="chat-input"
          />
          <button class="send-btn" aria-label="发送">发送</button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'
import KatoMascot from './KatoMascot.vue'

const modes = [
  { id: 'search', label: '检索知识', placeholder: '您可以用自然语言查找已有的知识', inputPlaceholder: '输入关键词或问题...' },
  { id: 'add', label: '新增知识', placeholder: '您可以输入文字/网址链接/拖入图片、视频、文件，我会帮您自动整理、提炼并分类', inputPlaceholder: '输入内容或拖入文件...' },
  { id: 'use', label: '使用知识', placeholder: '我可以帮您调用知识库内容写作，或输出总结报告', inputPlaceholder: '告诉我您想写什么或总结什么...' }
]

const currentMode = ref('search')

const currentPlaceholder = computed(() => {
  return modes.find(m => m.id === currentMode.value)?.placeholder || ''
})

const currentInputPlaceholder = computed(() => {
  return modes.find(m => m.id === currentMode.value)?.inputPlaceholder || ''
})
</script>

<style scoped>
.chat-section {
  max-width: 720px;
  margin: 0 auto 40px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.mascot-wrapper {
  margin-bottom: 20px;
  display: flex;
  justify-content: center;
}

.chat-container {
  width: 100%;
  background: var(--color-white);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-md);
  border: 1px solid var(--color-gray-200);
  overflow: hidden;
}

/* Tab 样式：融入聊天框顶部 */
.chat-tabs {
  display: flex;
  background: var(--color-gray-100);
  padding: 8px 16px 0;
  gap: 4px;
}

.tab-btn {
  padding: 12px 20px;
  border: none;
  border-radius: var(--radius) var(--radius) 0 0;
  font-size: 14px;
  color: var(--color-gray-600);
  cursor: pointer;
  transition: all 0.2s ease;
  font-family: inherit;
  background: transparent;
}

.tab-btn:hover {
  color: var(--color-green);
  background: rgba(82, 196, 26, 0.08);
}

.tab-btn.active {
  background: var(--color-white);
  color: var(--color-green);
  font-weight: 500;
  box-shadow: 0 -1px 2px rgba(0, 0, 0, 0.03);
}

.chat-body {
  background: var(--color-white);
  padding: 24px;
  min-height: 220px;
  display: flex;
  flex-direction: column;
}

.placeholder {
  font-size: 14px;
  color: var(--color-gray-600);
  line-height: 1.6;
  margin-bottom: 20px;
  flex: 1;
  min-height: 60px;
}

.input-area {
  display: flex;
  gap: 12px;
  margin-top: auto;
}

.chat-input {
  flex: 1;
  padding: 14px 18px;
  border: 1px solid var(--color-gray-200);
  border-radius: 24px;
  font-size: 14px;
  background: var(--color-gray-100);
  color: var(--color-gray-800);
  font-family: inherit;
}

.chat-input::placeholder {
  color: var(--color-gray-400);
}

.send-btn {
  padding: 14px 28px;
  background: var(--color-green);
  color: var(--color-white);
  border: none;
  border-radius: 24px;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  font-family: inherit;
  transition: background 0.2s;
  flex-shrink: 0;
}

.send-btn:hover {
  background: #389e0d;
}
</style>
