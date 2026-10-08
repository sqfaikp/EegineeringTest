<script setup>
const props = defineProps({
  modelValue: { type: Array, required: true }
})

const emit = defineEmits(['update:modelValue'])

function addInstrument() {
  const next = props.modelValue.concat({ id: Date.now(), name: '', model: '', sn: '' })
  emit('update:modelValue', next)
}

function removeInstrument(id) {
  emit(
    'update:modelValue',
    props.modelValue.filter((item) => item.id !== id)
  )
}

function updateInstrument(id, key, event) {
  const next = props.modelValue.map((item) =>
    item.id === id ? { ...item, [key]: event.target.value } : item
  )
  emit('update:modelValue', next)
}
</script>

<template>
  <section class="card">
    <div class="card__head">
      <div class="card__head-left">
        <span class="card__badge">02</span>
        <h3 class="card__title">仪器型号及唯一性编号</h3>
      </div>

      <button class="btn-add" type="button" @click="addInstrument">
        <svg viewBox="0 0 24 24" width="13" height="13" fill="none" stroke="currentColor"
          stroke-width="2.2" stroke-linecap="round">
          <path d="M12 5v14M5 12h14" />
        </svg>
        添加仪器
      </button>
    </div>

    <div v-for="(item, index) in modelValue" :key="item.id" class="inst">
      <div class="inst__grid inst__labels">
        <span></span>
        <span class="field__label">仪器名称</span>
        <span class="field__label">型号</span>
        <span class="field__label">编号</span>
        <span></span>
      </div>

      <div class="inst__grid">
        <span class="inst__num">{{ index + 1 }}</span>

        <input class="field__control" type="text" placeholder="如：钢筋扫描仪" :value="item.name"
          @input="updateInstrument(item.id, 'name', $event)" />
        <input class="field__control" type="text" placeholder="请输入型号" :value="item.model"
          @input="updateInstrument(item.id, 'model', $event)" />
        <input class="field__control" type="text" placeholder="请输入唯一性编号" :value="item.sn"
          @input="updateInstrument(item.id, 'sn', $event)" />

        <button class="btn-del" type="button" @click="removeInstrument(item.id)">删除</button>
      </div>
    </div>

    <p v-if="!modelValue.length" class="inst__empty">暂无仪器，点击右上角「添加仪器」新增一行</p>
  </section>
</template>

<style scoped>
.card {
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

.btn-add {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  height: 32px;
  padding: 0 12px;
  border: 1px solid #a9c6f5;
  border-radius: 6px;
  background: #fff;
  color: var(--blue);
  font-size: 12.5px;
  transition: 0.15s;
}

.btn-add:hover {
  background: #f4f8ff;
  border-color: #7fa9ef;
}

/* ---- 仪器行 ---- */
.inst + .inst {
  margin-top: 26px;
}

.inst__grid {
  display: grid;
  grid-template-columns: 28px minmax(0, 1.15fr) minmax(0, 1fr) minmax(0, 1fr) 72px;
  column-gap: 16px;
  align-items: center;
}

.inst__labels {
  margin-bottom: 8px;
}

.field__label {
  font-size: 12.5px;
  color: var(--text-2);
  line-height: 1;
}

.inst__num {
  width: 28px;
  height: 26px;
  border-radius: 6px;
  background: #eef4fe;
  color: var(--blue);
  font-size: 12px;
  font-weight: 600;
  display: grid;
  place-items: center;
}

.btn-del {
  height: 36px;
  border: 1px solid var(--input-border);
  border-radius: 6px;
  background: #fff;
  color: #6b7280;
  font-size: 12.5px;
  transition: 0.15s;
}

.btn-del:hover {
  border-color: #f0b3ae;
  color: var(--red);
  background: #fffafa;
}

.inst__empty {
  padding: 20px 0 4px;
  font-size: 12.5px;
  color: var(--text-3);
  text-align: center;
}
</style>
