<script setup lang="ts">
import { breakpointsTailwind, useBreakpoints } from '@vueuse/core'

const breakpoints = useBreakpoints(breakpointsTailwind)
const isMobile = breakpoints.smaller('sm') // only smaller than lg
const isAsideOpen = ref(false)
const isMini = ref(false)
const colorMode = useColorMode()

provide('isMini', isMini)

watchEffect(() => {
  isAsideOpen.value = !isMobile.value
})

function onMenuClick() {
  if (isMobile.value)
    isAsideOpen.value = false
}
</script>

<template>
  <VAppShell padded-container main-class="bg-slate-50 dark:bg-neutral-800" container-class="md:px-10">
    <template #header>
      <VAppBar shadow class="py-3 px-4 !flex lg:!hidden !z-[1]" size="auto" sticky>
        <VLogo :white="colorMode.preference !== 'light'" @click="onMenuClick" />
        <div class="flex-1" />
        <div class="flex items-center gap-3">
          <VBtn
            color="indigo"
            prefix-icon="ic:round-menu"
            @click="isAsideOpen = !isAsideOpen"
          />
        </div>
      </VAppBar>
    </template>

    <template #navigation>
      <AppBreadcrumbs />
    </template>

    <!-- aside -->
    <template #aside>
      <VNavDrawer
        v-model="isAsideOpen"
        v-model:mini="isMini"
        color="indigo"
        :fixed="isMobile"
        sticky
        :overlay="isMobile"
        :close-on-overlay-click="isMobile"
        :shadow="isMobile"
        :bordered="!isMobile"
        :class="[isMobile ? '[--nav-drawer-width:80%]' : '[--nav-drawer-width:300px]', { 'z-20': isMobile }]"
      >
        <div class="flex items-center gap-2 pr-2 pl-4 justify-between">
          <NuxtLink
            to="/"
            class="font-semibold border-indigo-900 border-b dark:border-neutral-700 h-[68px] lg:h-[60px] truncate flex items-center justify-center"
          >
            E-Commerce
          </NuxtLink>
          <VBtn
            v-if="!isMobile"
            color="indigo"
            prefix-icon="ic:round-menu"
            @click="isMini = !isMini"
          />
        </div>

        <div class="overflow-y-auto flex-1">
          <AppSidebarMenus @menu-click="onMenuClick" />
        </div>

        <!-- <AsideAccount /> -->
      </VNavDrawer>
    </template>

    <!-- content -->
    <slot />
    <template #content.after>
      <!-- <AdminFooter /> -->
    </template>
  </VAppShell>
</template>

<style lang="scss">
:root{
  --v-input-effect-border-color: var(--color-indigo-300) !important;
  --v-input-effect-shadow-color: var(--color-indigo-100) !important;
}
</style>
