<template>
  <div class="p-8 pt-4 flex flex-col gap-8">
    <div class="flex justify-between">
      <h1 class="text-3xl">Usuarios</h1>
      <UButton
        label="Crear nuevo"
        icon="i-heroicons-plus"
        @click="isCreateModalOpen = true" />
    </div>
    <table class="w-full">
      <thead class="bg-gray-100">
        <tr class="*:px-4 *:py-3">
          <th class="rounded-s-lg">Usuario</th>
          <th>Teléfono</th>
          <th>Documento</th>
          <th>Rol</th>
          <th>Estado</th>
          <th class="rounded-e-lg">Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="item in computedItems"
          class="*:px-4 *:py-2">
          <td>
            <div class="flex items-center gap-4">
              <UAvatar :text="item.name.slice(0, 1)"/>
              <div class="flex flex-col text-start">
                <span>{{ item.name }}</span>
                <span class="text-xs text-gray-400">{{ item.email }}</span>
              </div>
            </div>
          </td>
          <td class="text-center">{{ item.phoneNumber }}</td>
          <td class="text-center">{{ item.documentNumber }}</td>
          <td class="text-center">
            <UBadge
              v-if="item.isAdmin"
              label="Admin"
              variant="soft" />
            <UBadge
              v-else
              color="neutral"
              label="Inactivo"
              variant="soft" />
          </td>
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
            <UDropdownMenu
              :items="[
                {
                  label: 'Editar',
                  icon: 'i-heroicons-pencil-square-16-solid',
                  onSelect: () => {
                    isEditModalOpen = true;
                  },
                },
                {
                  label: 'Cambiar contraseña',
                  icon: 'i-heroicons-key-16-solid',
                  onSelect: () => {
                    isChangePasswordModalOpen = true;
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
        :total="1" />
    </div>

    <UModal
      v-model:open="isCreateModalOpen"
      title="Crear usuario">
      <template #body>
        <UsersCreateModal
          @close="
            () => {
              isCreateModalOpen = false;
            }
          " />
      </template>
    </UModal>

    <UModal
      v-model:open="isEditModalOpen"
      title="Editar usuario">
      <template #body>
        <UsersEditModal
          @close="
            () => {
              isEditModalOpen = false;
            }
          " />
      </template>
    </UModal>

    <UModal
      v-model:open="isChangePasswordModalOpen"
      title="Editar usuario">
      <template #body>
        <UsersChangePasswordModal
          @close="
            () => {
              isChangePasswordModalOpen = false;
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
const isChangePasswordModalOpen = ref(false);

const computedItems = computed(() => items.slice(page.value * 10 - 10, page.value * 10));

const items = [
  {
    name: 'Juan Esteban Becerra',
    email: 'jebecerrat@unadvirtual.edu.co',
    documentNumber: '1058350044',
    phoneNumber: '3125433587',
    active: true,
    isAdmin: true,
  },
];
</script>
