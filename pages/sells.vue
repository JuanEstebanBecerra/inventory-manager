<template>
  <div class="p-8 pt-4 flex flex-col gap-8">
    <div class="flex justify-between">
      <h1 class="text-3xl">Ventas</h1>
      <UButton
        label="Crear nuevo"
        icon="i-heroicons-plus"
        @click="isCreateModalOpen = true" />
    </div>
    <table class="w-full">
      <thead class="bg-gray-100">
        <tr class="*:px-4 *:py-3">
          <th class="rounded-s-lg">Fecha</th>
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
            {{ item.date }}
          </td>
          <td class="text-center">{{ item.items }}</td>
          <td class="text-center">
            <div class="flex items-center gap-4">
              <UAvatar :text="item.user.slice(0, 1)"/>
              <span>{{ item.user }}</span>
            </div>
          </td>
          <td class="text-center">
            <UBadge
              v-if="item.canceled"
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
                  label: 'Cancelar venta',
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
      title="Crear venta">
      <template #body>
        <SellsCreateModal
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
  { date: '01-Ene-2025', items: 20, user: 'Juan Esteban Becerra', canceled: false },
  { date: '02-Ene-2025', items: 12, user: 'Laura Martínez', canceled: false },
  { date: '03-Ene-2025', items: 17, user: 'Carlos Ramírez', canceled: true },
  { date: '04-Ene-2025', items: 23, user: 'Valentina Ríos', canceled: false },
  { date: '05-Ene-2025', items: 8, user: 'Andrés Gómez', canceled: false },
  { date: '06-Ene-2025', items: 19, user: 'Mariana López', canceled: true },
  { date: '07-Ene-2025', items: 14, user: 'Santiago Torres', canceled: false },
  { date: '08-Ene-2025', items: 25, user: 'Camila Herrera', canceled: false },
  { date: '09-Ene-2025', items: 16, user: 'Felipe Rodríguez', canceled: true },
  { date: '10-Ene-2025', items: 28, user: 'Daniela Castro', canceled: false },
  { date: '11-Ene-2025', items: 11, user: 'Mateo Sánchez', canceled: false },
  { date: '12-Ene-2025', items: 9, user: 'Natalia Vargas', canceled: false },
  { date: '13-Ene-2025', items: 33, user: 'Sebastián Pérez', canceled: true },
  { date: '14-Ene-2025', items: 21, user: 'Juliana Ruiz', canceled: false },
  { date: '15-Ene-2025', items: 18, user: 'Tomás Herrera', canceled: false },
  { date: '16-Ene-2025', items: 24, user: 'Isabella Gómez', canceled: false },
  { date: '17-Ene-2025', items: 29, user: 'Diego Morales', canceled: true },
  { date: '18-Ene-2025', items: 13, user: 'Sofía Medina', canceled: false },
  { date: '19-Ene-2025', items: 10, user: 'Emilio Vargas', canceled: false },
  { date: '20-Ene-2025', items: 32, user: 'Lucía Navarro', canceled: false },
  { date: '21-Ene-2025', items: 15, user: 'Gabriel Ortega', canceled: true },
  { date: '22-Ene-2025', items: 27, user: 'María José Duarte', canceled: false },
  { date: '23-Ene-2025', items: 22, user: 'David Salazar', canceled: false },
  { date: '24-Ene-2025', items: 19, user: 'Laura Sepúlveda', canceled: true },
  { date: '25-Ene-2025', items: 26, user: 'Alejandro Rivas', canceled: false },
  { date: '26-Ene-2025', items: 31, user: 'Nicole Mendoza', canceled: false },
  { date: '27-Ene-2025', items: 30, user: 'Samuel Patiño', canceled: true },
  { date: '28-Ene-2025', items: 35, user: 'Emma Cardona', canceled: false },
  { date: '29-Ene-2025', items: 16, user: 'Juanita Franco', canceled: false },
  { date: '30-Ene-2025', items: 20, user: 'Esteban Castaño', canceled: false },
  { date: '31-Ene-2025', items: 14, user: 'Ana María Correa', canceled: true },
  { date: '01-Feb-2025', items: 18, user: 'Andrés Restrepo', canceled: false },
  { date: '02-Feb-2025', items: 23, user: 'Mónica Quintero', canceled: false },
  { date: '03-Feb-2025', items: 13, user: 'Ricardo Peña', canceled: false },
  { date: '04-Feb-2025', items: 11, user: 'Sara Gutiérrez', canceled: false },
  { date: '05-Feb-2025', items: 17, user: 'Pablo Herrera', canceled: true },
  { date: '06-Feb-2025', items: 22, user: 'Antonia Suárez', canceled: false },
  { date: '07-Feb-2025', items: 25, user: 'Damián Uribe', canceled: false },
  { date: '08-Feb-2025', items: 20, user: 'Julieta Aguirre', canceled: false },
  { date: '09-Feb-2025', items: 12, user: 'Cristóbal Torres', canceled: true },
  { date: '10-Feb-2025', items: 24, user: 'Elena Zapata', canceled: false },
  { date: '11-Feb-2025', items: 19, user: 'Thiago Cárdenas', canceled: false },
  { date: '12-Feb-2025', items: 21, user: 'Martina Espinosa', canceled: false },
  { date: '13-Feb-2025', items: 15, user: 'Luciano Marín', canceled: true },
  { date: '14-Feb-2025', items: 26, user: 'Violeta Carrillo', canceled: false },
  { date: '15-Feb-2025', items: 29, user: 'Maximiliano Ruiz', canceled: false },
  { date: '16-Feb-2025', items: 30, user: 'Renata Molina', canceled: true },
  { date: '17-Feb-2025', items: 27, user: 'Tomás Londoño', canceled: false },
  { date: '18-Feb-2025', items: 28, user: 'Manuela Vargas', canceled: false },
  { date: '19-Feb-2025', items: 33, user: 'Juan Esteban Becerra', canceled: false },
];
</script>
