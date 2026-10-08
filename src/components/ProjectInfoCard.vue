<script setup>
import { standards } from '../data/forms.js'

const props = defineProps({
  modelValue: { type: Object, required: true }
})

const emit = defineEmits(['update:modelValue'])

function updateField(key, event) {
  emit('update:modelValue', { ...props.modelValue, [key]: event.target.value })
}
</script>

<template>
  <section class="card">
    <div class="card__head">
      <div class="card__head-left">
        <span class="card__badge">01</span>
        <h3 class="card__title">工程信息</h3>
      </div>
    </div>

    <div class="form-grid">
      <!-- 第一行 -->
      <label class="field">
        <span class="field__label">工程名称</span>
        <input class="field__control" type="text" placeholder="请输入工程名称"
          :value="modelValue.projectName" @input="updateField('projectName', $event)" />
      </label>

      <label class="field">
        <span class="field__label">合同编号</span>
        <input class="field__control" type="text" placeholder="请输入合同编号"
          :value="modelValue.contractNo" @input="updateField('contractNo', $event)" />
      </label>

      <label class="field">
        <span class="field__label">检测日期</span>
        <span class="field__date">
          <input class="field__control" type="text" placeholder="yyyy/mm/dd"
            :value="modelValue.testDate" @input="updateField('testDate', $event)" />
          <svg class="field__date-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor"
            stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
            <rect x="3" y="4" width="18" height="18" rx="2.5" />
            <path d="M16 2v4M8 2v4M3 10h18" />
          </svg>
        </span>
      </label>

      <!-- 第二行 -->
      <label class="field">
        <span class="field__label">工程地点</span>
        <input class="field__control" type="text" placeholder="请输入检测地点"
          :value="modelValue.location" @input="updateField('location', $event)" />
      </label>

      <label class="field">
        <span class="field__label">检测依据</span>
        <select class="field__control field__select" :value="modelValue.standard"
          @change="updateField('standard', $event)">
          <option v-for="s in standards" :key="s" :value="s">{{ s }}</option>
        </select>
      </label>
    </div>
  </section>
</template>

<style scoped>
.card {
  position: relative;
  background: #fff;
  border: 1px solid var(--border);
  border-radius: var(--radius);
  box-shadow: 0 1px 2px rgba(16, 24, 40, 0.03);
  padding: 18px 24px 24px;
}

.card__head {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 18px;
}

.card__head-left {
  display: flex;
  align-items: center;
  gap: 10px;
}

.card__badge {
  height: 22px;
  min-width: 30px;
  padding: 0 6px;
  border-radius: 5px;
  background: var(--navy-badge);
  color: #fff;
  font-size: 12px;
  font-weight: 600;
  letter-spacing: 0.5px;
  display: grid;
  place-items: center;
}

.card__title {
  font-size: 15px;
  font-weight: 600;
  color: #1a1f2b;
}

.form-grid {
  display: grid;
  grid-template-columns: minmax(0, 2.1fr) minmax(0, 0.95fr) minmax(0, 0.8fr);
  column-gap: 28px;
  row-gap: 16px;
}

.field {
  display: flex;
  flex-direction: column;
  gap: 8px;
  min-width: 0;
}

.field__label {
  font-size: 12.5px;
  color: var(--text-2);
  line-height: 1;
}

.field__date {
  position: relative;
  display: block;
}

.field__date-icon {
  position: absolute;
  right: 11px;
  top: 50%;
  transform: translateY(-50%);
  width: 15px;
  height: 15px;
  color: #909aa8;
  pointer-events: none;
}
</style>
