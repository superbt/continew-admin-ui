<template>
  <a-modal
    v-model:visible="visible"
    :title="title"
    :mask-closable="false"
    :esc-to-close="false"
    :width="width >= 500 ? 500 : '100%'"
    draggable
    @before-ok="save"
    @close="reset"
  >
    <GiForm ref="formRef" v-model="form" :options="options" :columns="columns" />
  </a-modal>
</template>

<script setup lang="ts">
import { Message } from '@arco-design/web-vue'
import { useWindowSize } from '@vueuse/core'
import { addApp, getApp, updateApp } from '@/apis/open/app'
import { type Columns, GiForm, type Options } from '@/components/GiForm'
import { useResetReactive } from '@/hooks'

const emit = defineEmits<{
  (e: 'save-success'): void
}>()

const { width } = useWindowSize()

const dataId = ref('')
const visible = ref(false)
const isUpdate = computed(() => !!dataId.value)
const title = computed(() => (isUpdate.value ? '修改应用' : '新增应用'))
const formRef = ref<InstanceType<typeof GiForm>>()

const options: Options = {
  form: { size: 'large' },
  btns: { hide: true },
}

const [form, resetForm] = useResetReactive({
  status: 1,
})

const columns: Columns = reactive([
  {
    label: '名称',
    field: 'name',
    type: 'input',
    rules: [{ required: true, message: '请输入名称' }],
  },
  {
    label: '失效时间',
    field: 'expireTime',
    type: 'date-picker',
    props: {
      placeholder: '请选择失效时间',
      showTime: true,
    },
  },
  {
    label: '描述',
    field: 'description',
    type: 'textarea',
    props: {
      maxLength: 200,
      autoSize: { minRows: 3, maxRows: 5 },
    },
  },
  {
    label: '状态',
    field: 'status',
    type: 'switch',
    props: {
      type: 'round',
      checkedValue: 1,
      uncheckedValue: 2,
      checkedText: '启用',
      uncheckedText: '禁用',
    },
  },
])

// 重置
const reset = () => {
  formRef.value?.formRef?.resetFields()
  resetForm()
}

// 保存
const save = async () => {
  try {
    const isInvalid = await formRef.value?.formRef?.validate()
    if (isInvalid) return false
    if (isUpdate.value) {
      await updateApp(form, dataId.value)
      Message.success('修改成功')
    } else {
      await addApp(form)
      Message.success('新增成功')
    }
    emit('save-success')
    return true
  } catch (error) {
    return false
  }
}

// 新增
const onAdd = () => {
  reset()
  dataId.value = ''
  visible.value = true
}

// 修改
const onUpdate = async (id: string) => {
  reset()
  dataId.value = id
  const { data } = await getApp(id)
  Object.assign(form, data)
  visible.value = true
}

defineExpose({ onAdd, onUpdate })
</script>
