<script setup lang="ts">
import type { VBreadcrumbItemProps } from '@morpheme/breadcrumbs'
import type { VDataTableHeader } from '@morpheme/table'
import { breakpointsTailwind, useBreakpoints } from '@vueuse/core'

useHead({
  title: 'Products',
})

definePageMeta({
  breadcrumbs: [
    {
      title: 'Products',
      to: '/products',
    },
  ] as VBreadcrumbItemProps[],
})

const breakpoints = useBreakpoints(breakpointsTailwind)
const isMobile = breakpoints.smaller('md') // only smaller than sm

const headers = ref<VDataTableHeader[]>([
  {
    text: 'Image',
    value: 'images',
  },
  {
    text: 'Name',
    value: 'name',
  },
  {
    text: 'Price',
    value: 'price',
  },
  {
    text: 'Category',
    value: 'category',
  },
  {
    text: 'Action',
    value: 'action',
    align: 'center',
    sortable: false,
  },
])

const items = ref([
  {
    id: 1,
    name: 'Smartphone',
    price: 599.99,
    category: 'Electronics',
    images: generateRandomPicsumImageLinks(3),
  },
  {
    id: 2,
    name: 'Laptop',
    price: 999.99,
    category: 'Electronics',
    images: generateRandomPicsumImageLinks(3),
  },
  {
    id: 3,
    name: 'Coffee Maker',
    price: 49.99,
    category: 'Kitchen Appliances',
    images: generateRandomPicsumImageLinks(2),
  },
  {
    id: 4,
    name: 'Running Shoes',
    price: 79.99,
    category: 'Footwear',
    images: generateRandomPicsumImageLinks(3),
  },
  {
    id: 5,
    name: 'HD TV',
    price: 799.99,
    category: 'Electronics',
    images: generateRandomPicsumImageLinks(2),
  },
  {
    id: 6,
    name: 'Desk Chair',
    price: 149.99,
    category: 'Furniture',
    images: generateRandomPicsumImageLinks(2),
  },
  {
    id: 7,
    name: 'Bluetooth Speaker',
    price: 69.99,
    category: 'Electronics',
    images: generateRandomPicsumImageLinks(2),
  },
  {
    id: 8,
    name: 'Digital Camera',
    price: 399.99,
    category: 'Electronics',
    images: generateRandomPicsumImageLinks(3),
  },
  {
    id: 9,
    name: 'Microwave Oven',
    price: 129.99,
    category: 'Kitchen Appliances',
    images: generateRandomPicsumImageLinks(2),
  },
  {
    id: 10,
    name: 'Running Shorts',
    price: 29.99,
    category: 'Clothing',
    images: generateRandomPicsumImageLinks(2),
  },
  {
    id: 11,
    name: 'Gaming Console',
    price: 499.99,
    category: 'Electronics',
    images: generateRandomPicsumImageLinks(2),
  },
  {
    id: 12,
    name: 'Coffee Table',
    price: 199.99,
    category: 'Furniture',
    images: generateRandomPicsumImageLinks(2),
  },
  {
    id: 13,
    name: 'Dumbbell Set',
    price: 89.99,
    category: 'Fitness Equipment',
    images: generateRandomPicsumImageLinks(2),
  },
  {
    id: 14,
    name: 'Hiking Backpack',
    price: 79.99,
    category: 'Outdoor Gear',
    images: generateRandomPicsumImageLinks(2),
  },
  {
    id: 15,
    name: 'Men\'s Watch',
    price: 149.99,
    category: 'Accessories',
    images: generateRandomPicsumImageLinks(2),
  },
  {
    id: 16,
    name: 'Women\'s Handbag',
    price: 69.99,
    category: 'Accessories',
    images: generateRandomPicsumImageLinks(2),
  },
  {
    id: 17,
    name: 'Digital Thermometer',
    price: 19.99,
    category: 'Health & Wellness',
    images: generateRandomPicsumImageLinks(1),
  },
  {
    id: 18,
    name: 'Kitchen Knife Set',
    price: 59.99,
    category: 'Kitchenware',
    images: generateRandomPicsumImageLinks(2),
  },
  {
    id: 19,
    name: 'Yoga Mat',
    price: 24.99,
    category: 'Fitness Equipment',
    images: generateRandomPicsumImageLinks(2),
  },
  {
    id: 20,
    name: 'Desk Lamp',
    price: 34.99,
    category: 'Home Decor',
    images: generateRandomPicsumImageLinks(2),
  },
])

function generateRandomPicsumImageLinks(count: number) {
  const imageLinks = []

  for (let i = 0; i < count; i++) {
    const imageURL = `https://picsum.photos/300/300?random=${i}`
    imageLinks.push(imageURL)
  }

  return imageLinks
}
</script>

<template>
  <AppPageHeader title="Products" subtitle="Manage your products here" />

  <VCard>
    <div class="flex w-full md:flex-no-wrap flex-wrap justify-between items-center gap-2 mb-5">
      <div>
        <VInput
          prepend-icon="ri:search-line"
          placeholder="Search"
        />
      </div>
      <VBtn color="indigo" prefix-icon="heroicons:plus-small-solid" :block="isMobile">
        Tambah
      </VBtn>
    </div>
    <VDataTable :headers="headers" :items="items" hover>
      <template #item.images="{ item }">
        <div class="overflow-hidden rounded-md w-12 h-12 object-cover">
          <NuxtImg :src="String(item.images[0])" />
        </div>
      </template>
      <template #item.action="{ item }">
        <TableActions :id="item.id" path="/products" />
      </template>
    </VDataTable>
  </VCard>
</template>
