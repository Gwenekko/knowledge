<template>
  <section class="knowledge-base">
    <div class="section-header">
      <h2>我的知识库</h2>
      <span class="manage-hint">可删除、新增、拖拽排序</span>
    </div>
    <div class="cards-grid">
      <div
        v-for="(item, index) in categories"
        :key="item.id"
        :class="['card', item.addMore ? 'add-more' : '']"
        @click="!item.addMore && onCardClick(item)"
      >
        <template v-if="item.addMore">
          <div class="add-more-icon">+</div>
          <span class="add-more-text">增加更多</span>
        </template>
        <template v-else>
          <div class="card-content">
            <div class="card-icon" :style="{ background: item.bgColor, color: item.iconColor }">
              <component :is="item.icon" />
            </div>
            <span class="card-title">{{ item.label }}</span>
            <span class="card-count">{{ item.count }} 条知识</span>
          </div>
        </template>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, h } from 'vue'

const BriefcaseIcon = () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.5' }, [
  h('path', { d: 'M20 7H4a2 2 0 0 0-2 2v10a2 2 0 0 0 2 2h16a2 2 0 0 0 2-2V9a2 2 0 0 0-2-2z' }),
  h('path', { d: 'M16 21V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v16' })
])

const CodeIcon = () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.5' }, [
  h('polyline', { points: '16 18 22 12 16 6' }),
  h('polyline', { points: '8 6 2 12 8 18' })
])

const HomeIcon = () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.5' }, [
  h('path', { d: 'm3 9 9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z' }),
  h('polyline', { points: '9 22 9 12 15 12 15 22' })
])

const BookIcon = () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.5' }, [
  h('path', { d: 'M4 19.5A2.5 2.5 0 0 1 6.5 17H20' }),
  h('path', { d: 'M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z' }),
  h('line', { x1: '8', y1: '6', x2: '16', y2: '6' }),
  h('line', { x1: '8', y1: '10', x2: '16', y2: '10' })
])

const LightbulbIcon = () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.5' }, [
  h('path', { d: 'M15 14c.2-1 .7-1.7 1.5-2.5 1-.9 1.5-2.2 1.5-3.5A6 6 0 0 0 6 8c0 1 .2 2.2 1.5 3.5.7.7 1.3 1.5 1.5 2.5' }),
  h('path', { d: 'M9 18h6' }),
  h('path', { d: 'M10 22h4' })
])

const StarIcon = () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.5' }, [
  h('polygon', { points: '12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2' })
])

const categories = ref([
  { id: '1', label: '职场必备', count: 12, icon: BriefcaseIcon, bgColor: '#e8f4fd', iconColor: '#5b9bd5' },
  { id: '2', label: '技术前沿', count: 8, icon: CodeIcon, bgColor: '#e6f7f0', iconColor: '#52a88a' },
  { id: '3', label: '生活技能', count: 15, icon: HomeIcon, bgColor: '#fef6e8', iconColor: '#c9a455' },
  { id: '4', label: '深度阅读', count: 6, icon: BookIcon, bgColor: '#f5ebe8', iconColor: '#a67c6b' },
  { id: '5', label: '灵感捕获', count: 23, icon: LightbulbIcon, bgColor: '#f3e8f5', iconColor: '#9b7bb3' },
  { id: '6', label: '私人收藏', count: 4, icon: StarIcon, bgColor: '#fce8ec', iconColor: '#c9808e' },
  { id: 'add', label: '', addMore: true }
])

const emit = defineEmits(['select'])

const onCardClick = (item) => {
  if (!item.addMore) emit('select', item)
}
</script>

<style scoped>
.knowledge-base {
  max-width: 960px;
  margin: 0 auto;
  padding: 0 24px 60px;
}

.section-header {
  display: flex;
  align-items: baseline;
  gap: 12px;
  margin-bottom: 24px;
}

.section-header h2 {
  font-size: 18px;
  font-weight: 600;
  color: var(--color-gray-800);
}

.manage-hint {
  font-size: 12px;
  color: var(--color-gray-400);
}

.cards-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
}

.card {
  aspect-ratio: 2 / 3;
  background: var(--color-white);
  border-radius: var(--radius);
  border: 1px solid var(--color-gray-200);
  box-shadow: var(--shadow-sm);
  padding: 24px;
  cursor: pointer;
  transition: all 0.2s ease;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.card:hover:not(.add-more) {
  border-color: var(--color-green);
  box-shadow: var(--shadow-md);
}

.card.add-more {
  border-style: dashed;
  border-color: var(--color-gray-400);
  background: var(--color-gray-100);
}

.card.add-more:hover {
  border-color: var(--color-green);
  background: var(--color-green-soft);
}

.card-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12px;
}

.card-icon {
  width: 48px;
  height: 48px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.card-icon svg {
  width: 24px;
  height: 24px;
}

.card-title {
  font-size: 16px;
  font-weight: 500;
  color: var(--color-gray-800);
}

.card-count {
  font-size: 12px;
  color: var(--color-gray-600);
}

.add-more-icon {
  font-size: 32px;
  color: var(--color-gray-400);
  margin-bottom: 8px;
  font-weight: 300;
}

.add-more-text {
  font-size: 14px;
  color: var(--color-gray-600);
}

@media (max-width: 768px) {
  .cards-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>
