<template>
  <div class="p-8 pt-4 flex flex-col gap-8">
    <div class="flex justify-between">
      <h1 class="text-3xl">Proveedores</h1>
      <UButton
        label="Crear nuevo"
        icon="i-heroicons-plus"
        @click="isCreateModalOpen = true" />
    </div>
    <table class="w-full">
      <thead class="bg-gray-100">
        <tr class="*:px-4 *:py-3">
          <th class="rounded-s-lg">Proveedor</th>
          <th>Correo</th>
          <th>Teléfono</th>
          <th>Estado</th>
          <th class="rounded-e-lg">Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="item in computedItems"
          class="*:px-4 *:py-2">
          <td>{{ item.name }}</td>
          <td class="text-center">{{ item.email }}</td>
          <td class="text-center">{{ item.phoneNumber }}</td>
          <td class="text-center">
            <UBadge
              v-if="item.active"
              color="success"
              label="Activo"
              variant="soft" />
            <UBadge
              v-else
              color="error"
              label="Inactivo"
              variant="soft" />
          </td>
          <td class="text-center">
            <UButton
              label="Editar"
              color="neutral"
              variant="outline"
              trailingIcon="i-heroicons-pencil-square-16-solid"
              @click="editItem(item)" />
          </td>
        </tr>
      </tbody>
    </table>
    <div class="flex justify-end">
      <UPagination
        v-model:page="page"
        :total="50" />
    </div>

    <UModal
      v-model:open="isCreateModalOpen"
      title="Crear proveedor">
      <template #body>
        <ProvidersCreateModal
          @close="
            () => {
              isCreateModalOpen = false;
            }
          " />
      </template>
    </UModal>

    <UModal
      v-model:open="isEditModalOpen"
      title="Editar proveedor">
      <template #body>
        <ProvidersEditModal
          :item="editModalItem"
          @close="
            () => {
              isEditModalOpen = false;
            }
          " />
      </template>
    </UModal>
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  layout: 'dashboard',
});

const page = ref(1);
const isCreateModalOpen = ref(false);
const isEditModalOpen = ref(false);
const editModalItem = ref();

const computedItems = computed(() => items.slice(page.value * 10 - 10, page.value * 10));

const editItem = (item: any) => {
  editModalItem.value = item;
  isEditModalOpen.value = true;
};

const items = [
  { name: 'Alimentos del Sur', email: 'contacto@alimentosdelsur.com', phoneNumber: '3001000001', active: true },
  { name: 'Comestibles Andinos', email: 'ventas@comestiblesandinos.com', phoneNumber: '3001000002', active: true },
  { name: 'Lácteos Nacionales', email: 'info@lacteosnacionales.com', phoneNumber: '3001000003', active: false },
  { name: 'Granos del Norte', email: 'granos@delnorte.com', phoneNumber: '3001000004', active: true },
  { name: 'Bebidas del Valle', email: 'servicio@bebidasvalle.com', phoneNumber: '3001000005', active: true },
  { name: 'Higiene Total', email: 'higiene@total.com', phoneNumber: '3001000006', active: false },
  { name: 'Productos del Campo', email: 'productos@campo.com', phoneNumber: '3001000007', active: true },
  { name: 'Panadería San Juan', email: 'panaderia@sanjuan.com', phoneNumber: '3001000008', active: true },
  { name: 'Distribuciones Gourmet', email: 'gourmet@distribuciones.com', phoneNumber: '3001000009', active: false },
  { name: 'Aseo Hogar', email: 'contacto@aseohogar.com', phoneNumber: '3001000010', active: true },
  { name: 'Agroindustrias del Llano', email: 'info@agrollano.com', phoneNumber: '3001000011', active: true },
  { name: 'Verduras Express', email: 'contacto@verdurax.com', phoneNumber: '3001000012', active: false },
  { name: 'Carnes Selectas', email: 'ventas@cselectas.com', phoneNumber: '3001000013', active: true },
  { name: 'Pescadería Azul', email: 'info@pazul.com', phoneNumber: '3001000014', active: true },
  { name: 'Café del Bosque', email: 'cafebosque@cafeteros.com', phoneNumber: '3001000015', active: false },
  { name: 'Licores del Valle', email: 'licores@valle.com', phoneNumber: '3001000016', active: true },
  { name: 'Pastas Italianas', email: 'ventas@pastasita.com', phoneNumber: '3001000017', active: true },
  { name: 'Azúcar Morena', email: 'contacto@azucarmorena.com', phoneNumber: '3001000018', active: false },
  { name: 'Aceites y Grasas', email: 'info@aceitesgrasas.com', phoneNumber: '3001000019', active: true },
  { name: 'Legumbres Selectas', email: 'ventas@legumselectas.com', phoneNumber: '3001000020', active: true },
  { name: 'Congelados del Sur', email: 'congelados@delsur.com', phoneNumber: '3001000021', active: true },
  { name: 'Bebidas Naturales', email: 'info@bebnaturales.com', phoneNumber: '3001000022', active: false },
  { name: 'Cereales y Más', email: 'ventas@cerealymas.com', phoneNumber: '3001000023', active: true },
  { name: 'Salsas del Mundo', email: 'contacto@salsasmundo.com', phoneNumber: '3001000024', active: false },
  { name: 'Vinagres Gourmet', email: 'info@vinagourmet.com', phoneNumber: '3001000025', active: true },
  { name: 'Panadería La Espiga', email: 'ventas@laespiga.com', phoneNumber: '3001000026', active: true },
  { name: 'Dulces y Delicias', email: 'contacto@dulcesdelicias.com', phoneNumber: '3001000027', active: true },
  { name: 'Helados del Bosque', email: 'helados@delbosque.com', phoneNumber: '3001000028', active: false },
  { name: 'Snacks y Pasabocas', email: 'ventas@snackspasabocas.com', phoneNumber: '3001000029', active: true },
  { name: 'Huevos del Campo', email: 'info@huevoscampo.com', phoneNumber: '3001000030', active: true },
  { name: 'Miel Natural', email: 'contacto@mielnatural.com', phoneNumber: '3001000031', active: true },
  { name: 'Frutas Selectas', email: 'info@frutaselectas.com', phoneNumber: '3001000032', active: false },
  { name: 'Verduras del Valle', email: 'ventas@verdurasvalle.com', phoneNumber: '3001000033', active: true },
  { name: 'Tubérculos Andinos', email: 'tuberculos@andinos.com', phoneNumber: '3001000034', active: true },
  { name: 'Granos y Semillas', email: 'info@granosemillas.com', phoneNumber: '3001000035', active: false },
  { name: 'Papel y Limpieza', email: 'ventas@papellimpieza.com', phoneNumber: '3001000036', active: true },
  { name: 'Cuidado Personal', email: 'contacto@cuidadopersonal.com', phoneNumber: '3001000037', active: true },
  { name: 'Limpieza Total', email: 'info@limpiezatotal.com', phoneNumber: '3001000038', active: false },
  { name: 'Ambientadores Fresh', email: 'ventas@freshambient.com', phoneNumber: '3001000039', active: true },
  { name: 'Cosméticos Naturales', email: 'info@cosmeticosnaturales.com', phoneNumber: '3001000040', active: true },
  { name: 'Farmacia Vida', email: 'ventas@farmaciavida.com', phoneNumber: '3001000041', active: true },
  { name: 'Lácteos de Montaña', email: 'contacto@lacteosmontaña.com', phoneNumber: '3001000042', active: false },
  { name: 'Conservas del Mar', email: 'info@conservasmar.com', phoneNumber: '3001000043', active: true },
  { name: 'Enlatados Express', email: 'ventas@enlatadosexpress.com', phoneNumber: '3001000044', active: true },
  { name: 'Carnes de Exportación', email: 'contacto@carnexport.com', phoneNumber: '3001000045', active: true },
  { name: 'Vegetales Hidropónicos', email: 'info@veghidro.com', phoneNumber: '3001000046', active: false },
  { name: 'Agua Pura', email: 'ventas@aguapura.com', phoneNumber: '3001000047', active: true },
  { name: 'Panadería y Café', email: 'contacto@panecafe.com', phoneNumber: '3001000048', active: true },
  { name: 'Especias del Mundo', email: 'info@especiasmundo.com', phoneNumber: '3001000049', active: false },
  { name: 'Aceites Gourmet', email: 'ventas@aceitesgourmet.com', phoneNumber: '3001000050', active: true },
];
</script>
