<template>
  <a-card
    class="general-card"
    title="快捷操作 xbt"
    :header-style="{ paddingBottom: '0' }"
    :body-style="{ padding: '24px 20px 16px 20px' }"
  >
    <a-row :gutter="8">
      <a-col
        v-for="link in links"
        :key="link.text"
        :span="8"
        class="wrapper"
        @click="router.replace({ path: link.path })"
      >
        <div class="icon">
          <GiSvgIcon :name="link.icon" />
        </div>
        <a-typography-paragraph class="text">
          {{ link.text }}
        </a-typography-paragraph>
      </a-col>
    </a-row>
  </a-card>
</template>

<script setup lang="ts">
const router = useRouter()

const links = [
  { text: '用户管理xbt', icon: 'user', path: '/system/user' },
  { text: '角色管理xbt', icon: 'user-group', path: '/system/role' },
  { text: '菜单管理xbt', icon: 'menu', path: '/system/menu' },
  { text: '文件管理xbt', icon: 'file', path: '/system/file' },
  { text: '代码生成xbt', icon: 'code', path: '/code/generator' },
  { text: '系统日志xbt', icon: 'history', path: '/monitor/log' },
]
</script>

<style scoped lang="less"></style>
