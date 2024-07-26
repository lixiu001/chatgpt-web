<script setup lang='ts'>
import { computed, onMounted } from 'vue'
import { NButton, NLayoutSider } from 'naive-ui'
import List from './List.vue'
import { useAppStore, useChatStore } from '@/store'

const appStore = useAppStore()
const chatStore = useChatStore()

const collapsed = computed(() => appStore.siderCollapsed)

async function handleAdd() {
  await chatStore.addNewHistory()
}

function handleUpdateCollapsed() {
  appStore.setSiderCollapsed(!collapsed.value)
}

onMounted(async () => {
})
</script>

<template>
  <NLayoutSider
    :collapsed="collapsed"
    :collapsed-width="0"
    :width="260"
    show-trigger="arrow-circle"
    collapse-mode="transform"
    position="absolute"
    bordered
    @update-collapsed="handleUpdateCollapsed"
  >
    <div class="flex flex-col h-full">
      <main class="flex flex-col flex-1 min-h-0">
        <div class="p-4">
          <NButton dashed block @click="handleAdd">
            {{ $t('chat.newChatButton') }}
          </NButton>
        </div>
        <div class="flex-1 min-h-0 pb-4 overflow-hidden">
          <List />
        </div>
      </main>
    </div>
  </NLayoutSider>
</template>

<style scoped>
.buttons-container {
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
}

.button-wrapper {
  margin-left: 10px;
}
</style>
