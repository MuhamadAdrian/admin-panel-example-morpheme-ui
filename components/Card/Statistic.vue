<script setup lang="ts">
import type { CardStats } from '~~/types'

interface Props {
  items: CardStats[]
}

const { items } = defineProps<Props>()

defineSlots<{
  'sub.value'?: (props: { item: CardStats }) => any
}>()
</script>

<template>
  <VCard v-for="stat in items" :key="stat.label" bodyless class="p-4">
    <div class="flex justify-between items-center">
      <h3 class="font-medium">
        {{ stat.label }}
      </h3>
      <VIcon :name="stat.icon" size="sm" class="text-gray-700" />
    </div>
    <div class="mt-3">
      <h2 class="text-2xl font-semibold">
        {{ stat.value }}
      </h2>
      <p class="text-sm text-gray-500 dark:text-neutral-500">
        <slot name="sub.value" :item="stat" />
      </p>
    </div>
  </VCard>
</template>
