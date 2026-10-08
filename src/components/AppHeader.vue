<script setup>
defineProps({
  subtitle: { type: String, default: '' }
})

const emit = defineEmits(['voice', 'save-draft', 'generate'])
</script>

<template>
  <header class="header">
    <div class="header__side"></div>

    <div class="header__main">
      <div class="header__inner">
        <div class="brand">
          <span class="brand__logo">检</span>
          <span class="brand__text">
            <span class="brand__title">工程检测记录</span>
            <span class="brand__sub">{{ subtitle }}</span>
          </span>
        </div>

        <div class="header__actions">
          <button class="hbtn hbtn--ghost" type="button" @click="emit('voice')">
            <svg class="hbtn__icon" viewBox="0 0 24 24" fill="none" stroke="currentColor"
              stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M12 2a3 3 0 0 0-3 3v6a3 3 0 0 0 6 0V5a3 3 0 0 0-3-3z" />
              <path d="M19 10v1a7 7 0 0 1-14 0v-1" />
              <path d="M12 18v4" />
            </svg>
            语音输入
          </button>

          <button class="hbtn hbtn--ghost" type="button" @click="emit('save-draft')">
            保存草稿
          </button>

          <button class="hbtn hbtn--primary" type="button" @click="emit('generate')">
            生成报告
          </button>
        </div>
      </div>
    </div>
  </header>
</template>

<style scoped>
.header {
  flex: 0 0 auto;
  height: 64px;
  display: flex;
  align-items: stretch;
  background: var(--navy);
  color: #fff;
}

.header__side {
  flex: 0 0 var(--sidebar-w);
  width: var(--sidebar-w);
}

.header__main {
  flex: 1;
  min-width: 0;
  padding: 0 var(--pad-x);
  display: flex;
  align-items: center;
}

.header__inner {
  width: 100%;
  max-width: var(--content-max);
  margin: 0 auto;
  display: flex;
  align-items: center;
  gap: 16px;
}

/* ---- 品牌区 ---- */
.brand {
  display: flex;
  align-items: center;
  gap: 10px;
  min-width: 0;
}

.brand__logo {
  flex: 0 0 30px;
  width: 30px;
  height: 30px;
  border: 1.5px solid rgba(255, 255, 255, 0.7);
  border-radius: 7px;
  display: grid;
  place-items: center;
  font-size: 15px;
  font-weight: 500;
  line-height: 1;
}

.brand__text {
  display: flex;
  flex-direction: column;
  gap: 2px;
  min-width: 0;
}

.brand__title {
  font-size: 17px;
  font-weight: 600;
  letter-spacing: 0.5px;
  line-height: 1.15;
}

.brand__sub {
  font-size: 11px;
  line-height: 1.1;
  color: rgba(255, 255, 255, 0.55);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

/* ---- 右侧操作 ---- */
.header__actions {
  margin-left: auto;
  display: flex;
  align-items: center;
  gap: 10px;
  flex: 0 0 auto;
}

.hbtn {
  height: 34px;
  padding: 0 14px;
  border-radius: 6px;
  font-size: 13px;
  display: inline-flex;
  align-items: center;
  gap: 6px;
  white-space: nowrap;
  transition: background 0.15s, border-color 0.15s, opacity 0.15s;
}

.hbtn__icon {
  width: 14px;
  height: 14px;
}

.hbtn--ghost {
  color: #fff;
  background: rgba(255, 255, 255, 0.06);
  border: 1px solid rgba(255, 255, 255, 0.3);
}

.hbtn--ghost:hover {
  background: rgba(255, 255, 255, 0.14);
  border-color: rgba(255, 255, 255, 0.55);
}

.hbtn--primary {
  color: #fff;
  background: #e5453b;
  border: 1px solid #e5453b;
  font-weight: 500;
}

.hbtn--primary:hover {
  background: #d43a30;
  border-color: #d43a30;
}
</style>
