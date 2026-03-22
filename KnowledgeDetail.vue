<template>
  <div class="knowledge-detail">
    <button class="back-btn" @click="$emit('back')">← 返回知识库</button>
    <h2 class="detail-title">{{ category?.label }}</h2>
    <div class="knowledge-list">
      <div
        v-for="item in mockKnowledge"
        :key="item.id"
        class="knowledge-card"
      >
        <div class="card-image" :style="{ background: item.bgColor }">
          <span v-if="!item.image">{{ item.type }}</span>
        </div>
        <div class="card-body">
          <h3 class="card-title">{{ item.title }}</h3>
          <p class="card-summary">{{ item.summary }}</p>
          <span class="card-date">{{ item.date }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  category: { type: Object, default: null }
})

defineEmits(['back'])

const mockKnowledge = computed(() => [
  { id: 1, title: '高效会议技巧总结', summary: '从议程设置到会后跟进，让每次会议都物有所值...', date: '2025-03-20', type: '文档', bgColor: 'linear-gradient(135deg, #e8f5e9 0%, #c8e6c9 100%)' },
  { id: 2, title: 'AI 辅助编程实践', summary: '如何用 Copilot 提升编码效率，结合实际项目经验...', date: '2025-03-18', type: '链接', bgColor: 'linear-gradient(135deg, #e3f2fd 0%, #bbdefb 100%)' },
  { id: 3, title: '产品需求文档模板', summary: '标准化的 PRD 结构，包含用户故事、验收标准...', date: '2025-03-15', type: '文档', bgColor: 'linear-gradient(135deg, #fff3e0 0%, #ffe0b2 100%)' }
])
</script>

<style scoped>
.knowledge-detail {
  max-width: 960px;
  margin: 0 auto;
  padding: 0 24px 60px;
}

.back-btn {
  background: none;
  border: none;
  color: var(--color-gray-600);
  font-size: 14px;
  cursor: pointer;
  margin-bottom: 20px;
  font-family: inherit;
}

.back-btn:hover {
  color: var(--color-green);
}

.detail-title {
  font-size: 20px;
  font-weight: 600;
  margin-bottom: 24px;
  color: var(--color-gray-800);
}

.knowledge-list {
  display: grid;
  gap: 20px;
}

.knowledge-card {
  display: flex;
  gap: 20px;
  background: var(--color-white);
  border-radius: var(--radius);
  border: 1px solid var(--color-gray-200);
  overflow: hidden;
  transition: box-shadow 0.2s;
}

.knowledge-card:hover {
  box-shadow: var(--shadow-md);
}

.card-image {
  width: 140px;
  min-height: 105px;
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 12px;
  color: var(--color-gray-600);
}

.card-body {
  flex: 1;
  padding: 20px 20px 20px 0;
}

.card-title {
  font-size: 16px;
  font-weight: 500;
  margin-bottom: 8px;
  color: var(--color-gray-800);
}

.card-summary {
  font-size: 14px;
  color: var(--color-gray-600);
  line-height: 1.5;
  margin-bottom: 8px;
}

.card-date {
  font-size: 12px;
  color: var(--color-gray-400);
}
</style>
