<script lang="ts" setup>
import { computed, watch } from 'vue';
import VueMarkdownEditor from '@kangc/v-md-editor';
import zhCN from '@kangc/v-md-editor/lib/lang/zh-CN';
import enUS from '@kangc/v-md-editor/lib/lang/en-US';
import { useLangStore } from '@/stores';

const lang = computed(() => {
  return useLangStore().lang;
});

const toolbar = {
  customToolbar: {},
};
const leftToolbar =
  'undo redo clear | h bold italic strikethrough quote | ul ol table hr | link image  preview ';
watch(
  () => lang.value,
  (val) => {
    val === 'zh'
      ? VueMarkdownEditor.lang.use('zh-CN', zhCN)
      : VueMarkdownEditor.lang.use('en-US', enUS);
  },
  { immediate: true }
);
</script>

<template>
  <v-md-editor
    mode="edit"
    :toolbar="toolbar"
    :left-toolbar="leftToolbar"
    :right-toolbar="''"
    :disabled-menus="[]"
    height="400px"
  ></v-md-editor>
</template>

<style lang="scss" scoped>
.v-md-editor {
  background-color: var(--o-color-bg4);
  box-shadow: none;
  border-radius: 0;
  border: 1px solid var(--o-color-border2);
  :deep(.v-md-editor__editor-wrapper) {
    border-right: 1px solid var(--o-color-border2);
  }

  :deep(textarea) {
    color: var(--o-color-text1);
    background-color: var(--o-color-bg2);
  }
  :deep(.v-md-editor__toolbar) {
    .v-md-editor__menu {
      border-radius: 0;
    }
    border: none;
    .v-md-editor__toolbar-item--active {
      background-color: var(--o-color-bg3);
    }
  }
  :deep(.vuepress-markdown-body) {
    margin: 0;
    padding: 20px 20px 30px;
    width: 100%;
    height: 100%;
    min-height: 358px;
    border: none;
    outline: none;
  }
}
</style>
