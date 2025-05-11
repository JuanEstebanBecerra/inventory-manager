<template>
  <div class="p-8 pt-4 flex flex-col gap-8">
    <div class="flex justify-between">
      <h1 class="text-3xl">Ingresos</h1>
      <UButton
        label="Crear nuevo"
        icon="i-heroicons-plus"
        @click="isCreateModalOpen = true" />
    </div>
    <table class="w-full">
      <thead class="bg-gray-100">
        <tr class="*:px-4 *:py-3">
          <th class="rounded-s-lg">Proveedor</th>
          <th>Fecha</th>
          <th>N. productos</th>
          <th>Usuario responsable</th>
          <th>Estado</th>
          <th class="rounded-e-lg">Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="item in computedItems"
          class="*:px-4 *:py-2">
          <td>
            {{ item.provider }}
          </td>
          <td>
            {{ item.date }}
          </td>
          <td class="text-center">{{ item.items }}</td>
          <td class="text-center">
            <div class="flex items-center gap-4">
              <UAvatar :text="item.user.slice(0, 1)" />
              <span>{{ item.user }}</span>
            </div>
          </td>
          <td class="text-center">
            <UBadge
              v-if="item.isCanceled"
              color="error"
              label="Cancelada"
              variant="soft" />
            <span
              v-else
              class="text-gray-400 text-sm"
              >Ninguno</span
            >
          </td>
          <td class="text-center">
            <UDropdownMenu
              :items="[
                {
                  label: 'Cancelar ingreso',
                  icon: 'i-heroicons-x-mark-16-solid',
                  onSelect: () => {
                    isWarningModalOpen = true;
                  },
                },
              ]">
              <UButton
                label="Acciones"
                color="neutral"
                variant="outline"
                trailing
                icon="i-heroicons-chevron-down-16-solid" />
            </UDropdownMenu>
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
      :ui="{
        content: ' max-w-4xl w-full h-[800px]',
      }"
      class="w-[500px]"
      v-model:open="isCreateModalOpen"
      title="Crear ingreso">
      <template #body>
        <EntrancesCreateModal
          @close="
            () => {
              isCreateModalOpen = false;
            }
          " />
      </template>
    </UModal>

    <WarningModal v-model:open="isWarningModalOpen" />
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  layout: 'dashboard',
});

const page = ref(1);
const isCreateModalOpen = ref(false);
const isWarningModalOpen = ref(false);

const computedItems = computed(() => items.slice(page.value * 10 - 10, page.value * 10));

const items = [
  { provider: 'Cárnicos del Norte', date: '01-Ene-2025', items: 20, user: 'Juan Esteban Becerra', isCanceled: false },
  { provider: 'Frutas Selectas', date: '02-Ene-2025', items: 12, user: 'Laura Martínez', isCanceled: false },
  { provider: 'Lácteos Andinos', date: '03-Ene-2025', items: 17, user: 'Carlos Ramírez', isCanceled: true },
  { provider: 'Cárnicos del Norte', date: '04-Ene-2025', items: 23, user: 'Valentina Ríos', isCanceled: false },
  { provider: 'Verduras Frescas', date: '05-Ene-2025', items: 8, user: 'Andrés Gómez', isCanceled: false },
  { provider: 'Panadería El Molino', date: '06-Ene-2025', items: 19, user: 'Mariana López', isCanceled: true },
  { provider: 'Frutas Selectas', date: '07-Ene-2025', items: 14, user: 'Santiago Torres', isCanceled: false },
  { provider: 'Cárnicos del Norte', date: '08-Ene-2025', items: 25, user: 'Camila Herrera', isCanceled: false },
  { provider: 'Verduras Frescas', date: '09-Ene-2025', items: 16, user: 'Felipe Rodríguez', isCanceled: true },
  { provider: 'Lácteos Andinos', date: '10-Ene-2025', items: 28, user: 'Daniela Castro', isCanceled: false },
  { provider: 'Frutas Selectas', date: '11-Ene-2025', items: 11, user: 'Mateo Sánchez', isCanceled: false },
  { provider: 'Cárnicos del Norte', date: '12-Ene-2025', items: 9, user: 'Natalia Vargas', isCanceled: false },
  { provider: 'Panadería El Molino', date: '13-Ene-2025', items: 33, user: 'Sebastián Pérez', isCanceled: true },
  { provider: 'Lácteos Andinos', date: '14-Ene-2025', items: 21, user: 'Juliana Ruiz', isCanceled: false },
  { provider: 'Verduras Frescas', date: '15-Ene-2025', items: 18, user: 'Tomás Herrera', isCanceled: false },
  { provider: 'Frutas Selectas', date: '16-Ene-2025', items: 24, user: 'Isabella Gómez', isCanceled: false },
  { provider: 'Cárnicos del Norte', date: '17-Ene-2025', items: 29, user: 'Diego Morales', isCanceled: true },
  { provider: 'Panadería El Molino', date: '18-Ene-2025', items: 13, user: 'Sofía Medina', isCanceled: false },
  { provider: 'Verduras Frescas', date: '19-Ene-2025', items: 10, user: 'Emilio Vargas', isCanceled: false },
  { provider: 'Frutas Selectas', date: '20-Ene-2025', items: 32, user: 'Lucía Navarro', isCanceled: false },
  { provider: 'Lácteos Andinos', date: '21-Ene-2025', items: 15, user: 'Gabriel Ortega', isCanceled: true },
  { provider: 'Panadería El Molino', date: '22-Ene-2025', items: 27, user: 'María José Duarte', isCanceled: false },
  { provider: 'Verduras Frescas', date: '23-Ene-2025', items: 22, user: 'David Salazar', isCanceled: false },
  { provider: 'Cárnicos del Norte', date: '24-Ene-2025', items: 19, user: 'Laura Sepúlveda', isCanceled: true },
  { provider: 'Frutas Selectas', date: '25-Ene-2025', items: 26, user: 'Alejandro Rivas', isCanceled: false },
  { provider: 'Panadería El Molino', date: '26-Ene-2025', items: 31, user: 'Nicole Mendoza', isCanceled: false },
  { provider: 'Verduras Frescas', date: '27-Ene-2025', items: 30, user: 'Samuel Patiño', isCanceled: true },
  { provider: 'Lácteos Andinos', date: '28-Ene-2025', items: 35, user: 'Emma Cardona', isCanceled: false },
  { provider: 'Frutas Selectas', date: '29-Ene-2025', items: 16, user: 'Juanita Franco', isCanceled: false },
  { provider: 'Cárnicos del Norte', date: '30-Ene-2025', items: 20, user: 'Esteban Castaño', isCanceled: false },
  { provider: 'Verduras Frescas', date: '31-Ene-2025', items: 14, user: 'Ana María Correa', isCanceled: true },
  { provider: 'Panadería El Molino', date: '01-Feb-2025', items: 18, user: 'Andrés Restrepo', isCanceled: false },
  { provider: 'Frutas Selectas', date: '02-Feb-2025', items: 23, user: 'Mónica Quintero', isCanceled: false },
  { provider: 'Cárnicos del Norte', date: '03-Feb-2025', items: 13, user: 'Ricardo Peña', isCanceled: false },
  { provider: 'Verduras Frescas', date: '04-Feb-2025', items: 11, user: 'Sara Gutiérrez', isCanceled: false },
  { provider: 'Lácteos Andinos', date: '05-Feb-2025', items: 17, user: 'Pablo Herrera', isCanceled: true },
  { provider: 'Panadería El Molino', date: '06-Feb-2025', items: 22, user: 'Antonia Suárez', isCanceled: false },
  { provider: 'Frutas Selectas', date: '07-Feb-2025', items: 25, user: 'Damián Uribe', isCanceled: false },
  { provider: 'Cárnicos del Norte', date: '08-Feb-2025', items: 20, user: 'Julieta Aguirre', isCanceled: false },
  { provider: 'Verduras Frescas', date: '09-Feb-2025', items: 12, user: 'Cristóbal Torres', isCanceled: true },
  { provider: 'Lácteos Andinos', date: '10-Feb-2025', items: 24, user: 'Elena Zapata', isCanceled: false },
  { provider: 'Panadería El Molino', date: '11-Feb-2025', items: 19, user: 'Thiago Cárdenas', isCanceled: false },
  { provider: 'Frutas Selectas', date: '12-Feb-2025', items: 21, user: 'Martina Espinosa', isCanceled: false },
  { provider: 'Cárnicos del Norte', date: '13-Feb-2025', items: 15, user: 'Luciano Marín', isCanceled: true },
  { provider: 'Verduras Frescas', date: '14-Feb-2025', items: 26, user: 'Violeta Carrillo', isCanceled: false },
  { provider: 'Lácteos Andinos', date: '15-Feb-2025', items: 29, user: 'Maximiliano Ruiz', isCanceled: false },
  { provider: 'Panadería El Molino', date: '16-Feb-2025', items: 30, user: 'Renata Molina', isCanceled: true },
  { provider: 'Frutas Selectas', date: '17-Feb-2025', items: 27, user: 'Tomás Londoño', isCanceled: false },
  { provider: 'Cárnicos del Norte', date: '18-Feb-2025', items: 28, user: 'Manuela Vargas', isCanceled: false },
  { provider: 'Verduras Frescas', date: '19-Feb-2025', items: 33, user: 'Juan Esteban Becerra', isCanceled: false },
];
</script>
