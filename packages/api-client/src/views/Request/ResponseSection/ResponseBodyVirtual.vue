<script setup lang="ts">
import ViewLayoutCollapse from '@/components/ViewLayout/ViewLayoutCollapse.vue'
import { ScalarVirtualText } from '@scalar/components'
import { formatJsonOrYamlString } from '@scalar/oas-utils/helpers'
import { computed } from 'vue'

const props = defineProps<{
  content: string
}>()

const textContent = computed(() => formatJsonOrYamlString(props.content))
</script>

<template>
  <ViewLayoutCollapse class="!max-h-[calc(100%-32px)] response-body-virtual">
    <template #title>Body</template>
    <div
      class="mx-1 py-1.5 px-2.5 font-code text-xxs border-1/2 rounded-t border-b-0">
      This response body is massive! Syntax highlighting won’t work here.
    </div>
    <ScalarVirtualText
      containerClass="custom-scroll scalar-code-block border-1/2 rounded-b flex flex-1 mx-1"
      contentClass="hljs language-plaintext"
      :lineHeight="20"
      :text="textContent" />
  </ViewLayoutCollapse>
</template>

<style>
.response-body-virtual[data-headlessui-state='open'],
.response-body-virtual[data-headlessui-state='open'] .diclosure-panel {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}
</style>
