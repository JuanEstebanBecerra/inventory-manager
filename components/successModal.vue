<template>
  <UModal v-model:open="openModel">
    <template #content>
      <div class="">
        <div class="flex flex-col items-center text-center px-8 pt-12 pb-0">
          <UIcon
            name="i-line-md-circle-twotone-to-confirm-circle-twotone-transition"
            class="w-16 h-16 mb-4 text-green-500" />
          <span class="text-xl font-bold">Éxito</span>
          <span>{{ props.description }}</span>
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

type Props = {
  description: string;
};

const props = defineProps<Props>();
</script>
