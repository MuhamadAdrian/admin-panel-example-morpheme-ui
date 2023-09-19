<script setup lang="ts">
import { Grid01Icon, PackageIcon, Wallet01Icon } from '@morphemeicons/vue/untitled'

const emit = defineEmits<{
  menuClick: [menu: MenuItem]
}>()

const isMini = inject<boolean>('isMini')

export interface MenuItem {
  text: string
  icon?: Component
  to?: string
  children?: MenuItem[]
}

const menus = ref<MenuItem[]>([
  {
    text: 'Home',
    to: '/',
    icon: Grid01Icon,
  },
  {
    text: 'Products',
    to: '/products',
    icon: PackageIcon,
  },
  {
    text: 'Transactions',
    to: '/transactions',
    icon: Wallet01Icon,
  },
])

const route = useRoute()

function isMenuActiveOnChildren(menu: MenuItem) {
  return menu.children?.some(child =>
    route.path.startsWith(String(child.to)),
  )
}

function onMenuClick(menu: MenuItem) {
  emit('menuClick', menu)
}
</script>

<template>
  <VList hover class="custom-list">
    <template v-for="menu in menus" :key="menu.text">
      <VListCollapse
        v-if="menu.children"
        :model-value="isMenuActiveOnChildren(menu)"
      >
        <template #activator="{ isOpen, toggle }">
          <VListItem
            append-icon="ri:arrow-down-s-line"
            :append-icon-class="isOpen ? 'rotate-180' : ''"
            exact-active-class="active"
            :class="{
              active: isMenuActiveOnChildren(menu),
            }"
            :hide-append="isMini"
            :hide-text="isMini"
            class="mb-1"
            @click="toggle"
          >
            <template #prepend>
              <component :is="menu.icon" class="w-7 h-7 text-current" />
            </template>
            {{ menu.text }}
          </VListItem>
        </template>
        <VList class="-mx-1">
          <VListItem
            v-for="child in menu.children"
            :key="child.text"
            :to="child.to"
            :hide-text="isMini"
            :hide-append="isMini"
            nuxt
            exact-active-class="active"
            @click="onMenuClick(child)"
          >
            <template #prepend>
              <component
                :is="child.icon"
                v-if="child.icon"
                class="w-7 h-7 text-current"
              />
            </template>
            {{ child.text }}
          </VListItem>
        </VList>
      </VListCollapse>
      <VListItem
        v-else
        :to="menu.to"
        :hide-text="isMini"
        :hide-append="isMini"
        nuxt
        exact-active-class="active"
        @click="onMenuClick(menu)"
      >
        <template #prepend>
          <component :is="menu.icon" class="w-7 h-7 text-current" />
        </template>
        {{ menu.text }}
      </VListItem>
    </template>
  </VList>
</template>

<style scoped lang="scss">
.custom-list {
  --v-list-item-color: var(--color-white);
  --v-list-item-hover-bg-color: var(--color-indigo-400);
  --v-list-item-hover-color: white;
}
.active {
  background-color: var(--color-indigo-500);
  color: var(--color-white);
  --v-list-item-icon-color: var(--color-white);
}
</style>
