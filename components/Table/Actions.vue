<script setup lang="ts">
const { path } = defineProps<{
  id?: string | number
  path?: string
}>()

const modalDeleteIsOpen = ref(false)

function onConfirm() {
  alert('Delete')
}
</script>

<template>
  <ClientOnly>
    <div class="flex items-center justify-center gap-2">
      <VBtn
        text
        fab
        :to="`${path}`"
        prefix-icon="untitled:eye"
      />
      <VBtn
        text
        fab
        :to="`${path}`"
        prefix-icon="untitled:edit-01"
      />
      <VBtn
        text
        fab
        prefix-icon="untitled:trash-01"
        @click="modalDeleteIsOpen = !modalDeleteIsOpen"
      />
    </div>

    <VModal
      v-model="modalDeleteIsOpen"
      title="Delete Item"
      confirm
      confirm-text="Delete"
      confirm-color="error"
      centered
      footer-class="flex-row-reverse"
      close-text="Cancel"
      @confirm="onConfirm"
    >
      <p>Are you sure want to delete this item?</p>
    </VModal>
  </ClientOnly>
</template>
