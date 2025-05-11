<template>
  <UModal v-model:open="openModel">
    <template #content>
      <div class="">
        <div class="flex flex-col items-center text-center px-8 pt-12 pb-0">
          <UIcon
            name="i-line-md-alert"
            class="w-16 h-16 mb-4 text-yellow-500" />
          <span class="text-xl font-bold">Advertencia</span>
          <span>¿Está seguro de que desea realizar esta acción?</span>
        </div>
        <div class="flex justify-end gap-4 items-center mt-4 w-full p-4">
          <UButton
            size="lg"
            label="Cancelar"
            color="neutral"
            variant="outline"
            @click="openModel = false" />
          <UButton
            label="Aceptar"
            size="lg"
            @click="openModel = false" />
        </div>
      </div>
    </template>
  </UModal>
</template>

<script setup lang="ts">
const openModel = defineModel<boolean>('open', { required: true });
</script>
