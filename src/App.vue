<script setup>
import { computed, ref, watch } from 'vue'
import AppHeader from './components/AppHeader.vue'
import LeftSidebar from './components/LeftSidebar.vue'
import ProjectInfoCard from './components/ProjectInfoCard.vue'
import InstrumentCard from './components/InstrumentCard.vue'
import SymbolBar from './components/SymbolBar.vue'
import { detectionItems } from './data/forms.js'

/** 左侧检测项目选中项 */
const activeId = ref(4)

const currentItem = computed(
  () => detectionItems.find((item) => item.id === activeId.value) || detectionItems[3]
)

/** 表单编号（与设计稿一致） */
const FORM_CODE = 'JL-J-G002'

/** 现场检测数据录入 —— 工程信息 */
const projectInfo = ref({
  projectName: '',
  contractNo: '',
  testDate: '',
  location: '',
  standard: 'GB50204-2015'
})

/** 仪器型号及唯一性编号 */
const instruments = ref([
  { id: 1, name: '', model: '', sn: '' },
  { id: 2, name: '', model: '', sn: '' }
])

/** 切换检测项目时重置录入内容 */
watch(activeId, () => {
  projectInfo.value = {
    projectName: '',
    contractNo: '',
    testDate: '',
    location: '',
    standard: 'GB50204-2015'
  }
  instruments.value = [
    { id: Date.now(), name: '', model: '', sn: '' },
    { id: Date.now() + 1, name: '', model: '', sn: '' }
  ]
})

/* ---------- 轻提示 ---------- */
const toast = ref('')
let toastTimer = null

function showToast(message) {
  toast.value = message
  clearTimeout(toastTimer)
  toastTimer = setTimeout(() => (toast.value = ''), 2000)
}

function handleVoice() {
  showToast('语音输入已开启，请开始讲话…')
}

function handleSaveDraft() {
  showToast('草稿已保存')
}

function handleGenerate() {
  showToast('正在生成检测报告…')
}

function handleStart() {
  showToast('确认工程与仪器信息后进入构件检测')
}

function handleSymbol(symbol) {
  showToast(`已选中符号：${symbol}`)
}
</script>

<template>
  <div class="app">
    <AppHeader :subtitle="currentItem.name" @voice="handleVoice" @save-draft="handleSaveDraft"
      @generate="handleGenerate" />

    <div class="app__body">
      <LeftSidebar v-model="activeId" :items="detectionItems" />

      <main class="app__main">
        <div class="app__scroller">
          <div class="content">
            <div class="page-head">
              <div class="page-head__left">
                <p class="eyebrow">现场检测数据录入</p>
                <h1 class="page-title">{{ currentItem.title }}</h1>
              </div>
              <p class="page-code">表单编号：{{ FORM_CODE }}</p>
            </div>

            <ProjectInfoCard v-model="projectInfo" />
            <InstrumentCard v-model="instruments" />

            <div class="start-area">
              <button class="btn-start" type="button" @click="handleStart">
                开始检测
                <svg viewBox="0 0 24 24" width="19" height="19" fill="none" stroke="currentColor"
                  stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M4 12h15" />
                  <path d="m13 6 6 6-6 6" />
                </svg>
              </button>
              <p class="start-hint">确认工程与仪器信息后进入构件检测</p>
            </div>
          </div>
        </div>
      </main>
    </div>

    <SymbolBar @insert="handleSymbol" />

    <Transition name="toast">
      <div v-if="toast" class="toast">{{ toast }}</div>
    </Transition>
  </div>
</template>

<style scoped>
.app {
  display: flex;
  flex-direction: column;
  height: 100vh;
  overflow: hidden;
}

.app__body {
  flex: 1;
  min-height: 0;
  display: flex;
}

.app__main {
  flex: 1;
  min-width: 0;
  min-height: 0;
  overflow: hidden;
  display: flex;
}

.app__scroller {
  flex: 1;
  min-width: 0;
  overflow-y: auto;
  padding: 24px var(--pad-x) 40px;
}

.content {
  width: 100%;
  max-width: var(--content-max);
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 18px;
}

/* ---- 页面标题 ---- */
.page-head {
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
  gap: 24px;
  padding-bottom: 2px;
}

.eyebrow {
  font-size: 12px;
  color: var(--text-3);
  margin-bottom: 7px;
}

.page-title {
  font-size: 25px;
  font-weight: 700;
  color: #12161f;
  letter-spacing: 0.5px;
  line-height: 1.2;
}

.page-code {
  font-size: 12.5px;
  color: var(--text-3);
  white-space: nowrap;
  padding-bottom: 3px;
}

/* ---- 开始检测 ---- */
.start-area {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 11px;
  margin-top: 18px;
  padding-bottom: 8px;
}

.btn-start {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  height: 48px;
  padding: 0 40px;
  border-radius: 9px;
  background: var(--red-deep);
  color: #fff;
  font-size: 16px;
  font-weight: 600;
  letter-spacing: 1px;
  box-shadow: 0 6px 16px rgba(203, 49, 41, 0.22);
  transition: 0.15s;
}

.btn-start:hover {
  background: #bd2b23;
  box-shadow: 0 8px 20px rgba(203, 49, 41, 0.3);
}

.btn-start:active {
  transform: translateY(1px);
}

.start-hint {
  font-size: 12px;
  color: var(--text-3);
}

/* ---- toast ---- */
.toast {
  position: fixed;
  left: 50%;
  bottom: 76px;
  transform: translateX(-50%);
  padding: 9px 18px;
  border-radius: 8px;
  background: rgba(26, 31, 43, 0.88);
  color: #fff;
  font-size: 13px;
  z-index: 50;
  pointer-events: none;
}

.toast-enter-active,
.toast-leave-active {
  transition: opacity 0.22s, transform 0.22s;
}

.toast-enter-from,
.toast-leave-to {
  opacity: 0;
  transform: translateX(-50%) translateY(6px);
}
</style>
