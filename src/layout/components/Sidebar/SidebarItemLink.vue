<script lang="ts" setup>
import { useRouter } from "vue-router"
import { isExternal } from "@/utils/validate"

const props = defineProps({
  to: {
    type: String,
    required: true
  }
})

const router = useRouter()

const push = () => {
  router.push(props.to).catch((err) => {
    console.warn(err)
  })
}
</script>

<template>
  <!-- 判断是否是外链(http/https/ftp)，如果是外链利用a标签跳转 -->
  <a v-if="isExternal(to)" :href="to" target="_blank" rel="noopener">
    <slot />
  </a>
  <!-- 非外链走vue路由 -->
  <div v-else @click="push">
    <slot />
  </div>
</template>
