<script setup lang="ts">
import type { CardStats } from '~/types'

useHead({
  title: 'Dashboard',
})

const stats = ref<CardStats[]>([
  {
    label: 'Total Revenue',
    icon: 'ph:currency-circle-dollar-bold',
    value: '$45,231.89',
    notes: '+20.1% from last month',
  },
  {
    label: 'Transactions',
    icon: 'tdesign:undertake-transaction',
    value: '+2350',
    notes: '+180.1% from last month',
  },
  {
    label: 'Categories',
    icon: 'iconamoon:category-light',
    value: '142',
    notes: '+19% from last month',
  },
  {
    label: 'Cancelled',
    icon: 'mdi:cancel-bold',
    value: '2',
    notes: '+0,0002% since last hour',
  },
])
</script>

<template>
  <AppPageHeader title="Dashboard" subtitle="Monitor your metrics for shipping, transactions, product and many more in here" />

  <div class="grid md:grid-cols-4 gap-4">
    <CardStatistic :items="stats">
      <template #sub.value="{ item }">
        {{ item.notes }}
      </template>
    </CardStatistic>
    <div class="md:col-span-2">
      <!-- <DashboardChart /> -->
    </div>
  </div>
</template>
