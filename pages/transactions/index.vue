<script setup lang="ts">
import type { VBreadcrumbItemProps } from '@morpheme/breadcrumbs'
import type { VDataTableHeader } from '@morpheme/table'

useHead({
  title: 'Transactions',
})

definePageMeta({
  breadcrumbs: [
    {
      title: 'Transactions',
      to: '/transactions',
    },
  ] as VBreadcrumbItemProps[],
})

const selectedTab = ref(0)

const headers = ref<VDataTableHeader[]>([
  {
    text: 'Order Number',
    value: 'order-number',
  },
  {
    text: 'Product Name',
    value: 'name',
  },
  {
    text: 'Quantity',
    value: 'quantity',
  },
  {
    text: 'Phone Number',
    value: 'phone',
  },
  {
    text: 'Address',
    value: 'address',
  },
])

const items = ref([
  {
    text: 'Tab Item 1',
  },
  {
    text: 'Tab Item 2',
  },
  {
    text: 'Tab Item 3',
  },
])
</script>

<template>
  <AppPageHeader title="Transactions" subtitle="Monitor your transaction here" />

  <VCard body-class="!p-0" hide-footer hide-header>
    <VTabs v-model="selectedTab" :items="items" active-class="!text-indigo-500" slider-class="!border-indigo-500" />

    <div class="p-4">
      <div v-if="selectedTab === 0">
        <h3 class="text-lg mb-2 font-semibold">
          Pending
        </h3>
        <VDataTable :headers="headers" :items="[]" />
      </div>
      <div v-if="selectedTab === 1">
        <h3 class="text-lg mb-2 font-semibold">
          Sending
        </h3>
        <VDataTable :headers="headers" :items="[]" />
      </div>
      <div v-if="selectedTab === 2">
        <h3 class="text-lg mb-2 font-semibold">
          Complete
        </h3>
        <VDataTable :headers="headers" :items="[]" />
      </div>
    </div>
  </VCard>
</template>
