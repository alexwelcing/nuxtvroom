<script setup lang="ts">
import { onMounted, ref } from 'vue'
import ThreeCube from '~/components/ThreeCube.vue'

const online = useOnline()
const contents = ref([])

onMounted(async () => {
  contents.value = await fetch('/')
})
</script>

<template>
  <div>
    <Logos mb-6 />
    <Suspense>
      <ClientOnly>
        <PageView v-if="online" />
        <div v-else text-gray:80>
          You're offline
        </div>
      </ClientOnly>
      <template #fallback>
        <div italic op50>
          <span animate-pulse>Loading...</span>
        </div>
      </template>
    </Suspense>
    <InputEntry />
    <ThreeCube />
    <div v-for="content in contents" :key="content.slug">
      {{ content.title }}
    </div>
  </div>
</template>
