<script setup>
import { rebarSymbols, axisSymbols } from '../data/forms.js'

const emit = defineEmits(['insert'])

function pick(symbol) {
  emit('insert', symbol)
}
</script>

<template>
  <footer class="symbolbar">
    <div class="symbolbar__side"></div>

    <div class="symbolbar__main">
      <div class="symbolbar__inner">
        <span class="symbolbar__label">钢筋符号</span>
        <button v-for="(s, i) in rebarSymbols" :key="'r' + i" type="button" class="chip"
          @click="pick(s)">
          {{ s }}
        </button>

        <span class="symbolbar__label symbolbar__label--gap">轴线</span>
        <button v-for="a in axisSymbols" :key="a" type="button" class="chip" @click="pick(a)">
          {{ a }}
        </button>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.symbolbar {
  flex: 0 0 auto;
  height: 48px;
  display: flex;
  align-items: stretch;
  border-top: 1px solid var(--border);
  background: #fff;
}

.symbolbar__side {
  flex: 0 0 var(--sidebar-w);
  width: var(--sidebar-w);
}

.symbolbar__main {
  flex: 1;
  min-width: 0;
  padding: 0 var(--pad-x);
  display: flex;
  align-items: center;
}

.symbolbar__inner {
  width: 100%;
  max-width: var(--content-max);
  margin: 0 auto;
  display: flex;
  align-items: center;
  gap: 6px;
  overflow-x: auto;
  scrollbar-width: none;
}

.symbolbar__inner::-webkit-scrollbar {
  display: none;
}

.symbolbar__label {
  flex: 0 0 auto;
  font-size: 12px;
  color: var(--text-2);
  margin-right: 6px;
  white-space: nowrap;
}

.symbolbar__label--gap {
  margin-left: 22px;
}

.chip {
  flex: 0 0 auto;
  width: 23px;
  height: 23px;
  border: 1px solid #e2e5ea;
  border-radius: 4px;
  background: #fafbfc;
  color: #606266;
  font-size: 13px;
  line-height: 1;
  display: grid;
  place-items: center;
  transition: 0.15s;
}

.chip:hover {
  border-color: #a9c6f5;
  background: #f4f8ff;
  color: var(--blue);
}
</style>
