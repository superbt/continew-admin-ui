<template>
  <a-modal v-model:visible="visible" :width="width >= 600 ? 'auto' : '100%'" :footer="false" draggable @close="reset">
    <a-typography :style="{ marginTop: '-40px', textAlign: 'center' }">
      <a-typography-title>
        {{ dataDetail?.title }}
      </a-typography-title>
      <a-typography-paragraph>
        <div class="meta-data">
          <a-space>
            <span>
              <icon-user class="icon" />
              <span class="label">发布人xbt：</span>
              <span>{{ dataDetail?.createUserString }}</span>
            </span>
            <a-divider direction="vertical" />
            <span>
              <icon-history class="icon" />
              <span class="label">发布时间xbt：</span>
              <span>{{ dataDetail?.effectiveTime ? dataDetail?.effectiveTime : dataDetail?.createTime }}</span>
            </span>
          </a-space>
        </div>
      </a-typography-paragraph>
    </a-typography>
    <a-divider />
    <AiEditor :model-value="dataDetail?.content" />
    <a-divider />
    <div v-if="dataDetail?.updateTime" class="update-time-row">
      <span>
        <icon-schedule class="icon" />
        <span>最后更新于：</span>
        <span>{{ dataDetail?.updateTime }}</span>
      </span>
    </div>
  </a-modal>
</template>

<script setup lang="ts">
import { useWindowSize } from '@vueuse/core'
import AiEditor from './detail/components/index.vue'
import { type NoticeResp, getNotice } from '@/apis/system'

const { width } = useWindowSize()
const dataDetail = ref<NoticeResp>({
  content: '',
})
const visible = ref(false)
// 详情
const onDetail = async (id: string) => {
  const { data } = await getNotice(id)
  dataDetail.value = data
  visible.value = true
}

// 重置
const reset = () => {
  dataDetail.value = {
    content: '',
  }
}

defineExpose({ onDetail })
</script>

<style scoped lang="scss">
.arco-link {
  color: rgb(var(--gray-8));
}

.icon {
  margin-right: 3px;
}

.update-time-row {
  text-align: right;
}
</style>
