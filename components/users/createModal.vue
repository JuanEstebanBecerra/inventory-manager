<template>
  <div class="flex flex-col gap-4">
    <UFormField label="Nombre">
      <UInput
        class="w-full"
        placeholder="Nombre del producto" />
    </UFormField>
    <div class="grid grid-cols-2 gap-4">
      <UFormField label="Correo">
        <UInput
          class="w-full"
          placeholder="user@unadvirtual.edu.co" />
      </UFormField>
      <UFormField label="Teléfono">
        <UInput
          class="w-full"
          placeholder="xxx xxx xx xx" />
      </UFormField>
    </div>
    <UFormField label="Número de documento">
      <UInput
        class="w-full"
        placeholder="xxx.xxx.xx.xx" />
    </UFormField>
    <UFormField
      label="Contraseña"
      hint="Mínimo 8 caracteres">
      <UInput
        class="w-full"
        placeholder="********" />
    </UFormField>
    <UFormField
      label="Confirmar contraseña"
      hint="Mínimo 8 caracteres">
      <UInput
        class="w-full"
        placeholder="********" />
    </UFormField>
    <UFormField label="Admin">
      <div class="flex items-center gap-4">
        <UCheckbox v-model="isAdmin" />
        {{ isAdmin ? 'Si' : 'No' }}
      </div>
    </UFormField>

    <div class="flex justify-end items-center gap-4 mt-4">
      <UButton
        size="lg"
        color="neutral"
        label="Cancelar"
        variant="outline"
        @click="emit('close')" />
      <UButton
        size="lg"
        label="Guardar"
        @click="emit('close')" />
    </div>
  </div>
</template>

<script setup lang="ts">
type Emits = (e: 'close') => void;

const emit = defineEmits<Emits>();

const isAdmin = ref(false);
</script>
