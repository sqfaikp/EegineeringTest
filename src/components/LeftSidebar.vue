<script setup>
defineProps({
  items: { type: Array, required: true },
  modelValue: { type: Number, required: true }
})

const emit = defineEmits(['update:modelValue'])
</script>

<template>
  <aside class="sidebar">
    <div class="sidebar__head">
      <h2 class="sidebar__title">检测项目</h2>
      <p class="sidebar__sub">选择录入表单</p>
      <button class="sidebar__collapse" type="button" title="收起">
        <svg viewBox="0 0 24 24" width="13" height="13" fill="none" stroke="currentColor"
          stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round">
          <path d="m15 18-6-6 6-6" />
        </svg>
      </button>
    </div>

    <nav class="sidebar__list">
      <button v-for="item in items" :key="item.id" type="button" class="sidebar__item"
        :class="{ 'is-active': item.id === modelValue }" @click="emit('update:modelValue', item.id)">
        <span class="sidebar__num">{{ item.id }}</span>
        <span class="sidebar__name">{{ item.name }}</span>
      </button>
    </nav>
  </aside>
</template>

<style scoped>
.sidebar {
  flex: 0 0 var(--sidebar-w);
  width: var(--sidebar-w);
  min-height: 0;
  display: flex;
  flex-direction: column;
  border-right: 1px solid var(--border);
  background: #fff;
}

.sidebar__head {
  position: relative;
  padding: 20px 16px 10px;
}

.sidebar__title {
  font-size: 15px;
  font-weight: 600;
  color: #1a1f2b;
  line-height: 1.2;
}

.sidebar__sub {
  margin-top: 5px;
  font-size: 11px;
  color: #a5abb6;
  line-height: 1.2;
}

.sidebar__collapse {
  position: absolute;
  top: 18px;
  right: 14px;
  width: 22px;
  height: 22px;
  border: 1px solid var(--border);
  border-radius: 50%;
  background: #fff;
  color: var(--text-3);
  display: grid;
  place-items: center;
  transition: 0.15s;
}

.sidebar__collapse:hover {
  background: #f5f6f8;
  color: var(--text-2);
}

.sidebar__list {
  flex: 1;
  min-height: 0;
  overflow-y: auto;
  padding: 6px 12px 20px;
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.sidebar__item {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 9px 10px;
  border: 1px solid transparent;
  border-radius: 7px;
  text-align: left;
  font-size: 12px;
  line-height: 1.45;
  color: var(--text-2);
  transition: background 0.15s, color 0.15s, border-color 0.15s;
}

.sidebar__item:hover {
  background: #f6f8fb;
}

.sidebar__num {
  flex: 0 0 18px;
  height: 18px;
  border-radius: 5px;
  background: #f1f3f6;
  color: #9aa1ac;
  font-size: 10.5px;
  font-weight: 500;
  display: grid;
  place-items: center;
  transition: 0.15s;
}

.sidebar__name {
  min-width: 0;
}

.sidebar__item.is-active {
  background: var(--blue-soft);
  border-color: var(--blue-line);
  color: var(--blue);
  font-weight: 600;
}

.sidebar__item.is-active .sidebar__num {
  background: #d6e6ff;
  color: var(--blue);
}
</style>
