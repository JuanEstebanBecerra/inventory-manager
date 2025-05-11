<template>
  <div class="flex flex-col gap-4">
    <UFormField label="Nombre">
      <UInput
        class="w-full"
        placeholder="Nombre del producto" />
    </UFormField>
    <div class="grid grid-cols-2 gap-4">
      <UFormField label="Proveedor">
        <USelectMenu
          class="w-full"
          placeholder="Seleccione"
          :items="providers"
          valueKey="id" />
      </UFormField>
      <UFormField label="Código de producto">
        <UInput
          class="w-full"
          placeholder="xxxxxxxx" />
      </UFormField>
    </div>
    <UFormField label="Cantidad">
      <UInput
        class="w-full"
        placeholder="Ej. 10" />
    </UFormField>
    <UFormField label="Precio">
      <UInput
        class="w-full"
        placeholder="Ej. 10.000" />
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

const providers = [
  { id: 1, label: 'Alimentos del Sur' },
  { id: 2, label: 'Comestibles Andinos' },
  { id: 3, label: 'Lácteos Nacionales' },
  { id: 4, label: 'Granos del Norte' },
  { id: 5, label: 'Bebidas del Valle' },
  { id: 6, label: 'Higiene Total' },
  { id: 7, label: 'Productos del Campo' },
  { id: 8, label: 'Panadería San Juan' },
  { id: 9, label: 'Distribuciones Gourmet' },
  { id: 10, label: 'Aseo Hogar' },
];
</script>
