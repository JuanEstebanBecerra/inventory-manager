<template>
  <div class="flex w-screen h-screen">
    <div class="w-[300px] h-full bg-white border-r border-gray-200 flex flex-col p-4 gap-4 flex-none">
      <div class="flex items-center gap-4 mb-8">
        <UIcon
          class="w-8 h-8"
          name="i-material-symbols-package-2" />
        <h1 class="text-lg">Inventory Manager</h1>
      </div>
      <UButton
        v-for="item in sidebarItems"
        :label="item.label"
        :icon="item.icon"
        size="xl"
        class="text-start"
        variant="ghost"
        color="neutral"
        :to="item.to"
        activeColor="primary"
        activeVariant="solid" />
      <div class="flex-1"></div>
      <UButton
        v-for="item in sidebarBottomItems"
        :label="item.label"
        :icon="item.icon"
        size="xl"
        class="text-start"
        variant="ghost"
        color="neutral"
        :to="item.to"
        activeColor="primary"
        activeVariant="solid" />
    </div>
    <div class="flex flex-col flex-1">
      <div class="flex-none w-full flex justify-end px-8 py-4">
        <UDropdownMenu
          :items="dropdownItems"
          :ui="{
            content: 'w-48',
          }">
          <UButton
            icon="i-material-symbols-person-rounded"
            color="neutral"
            variant="ghost" />
        </UDropdownMenu>
      </div>
      <slot class="flex-1 h-full"></slot>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { DropdownMenuItem } from '@nuxt/ui';

const dropdownItems = ref<DropdownMenuItem[][]>([
  [
    {
      label: 'Esteban Becerra',
      avatar: {
        src: 'https://github.com/juanestebanbecerra.png',
      },
      type: 'label',
    },
  ],
  [
    {
      label: 'Cerrar sesión',
      icon: 'i-lucide-log-out',
      to: '/login',
    },
  ],
]);

const sidebarItems = [
  {
    label: 'Ventas',
    icon: 'i-material-symbols-receipt-outline-rounded',
    to: 'sells',
  },
  {
    label: 'Proveedores',
    icon: 'i-material-symbols-storefront-outline',
    to: 'providers',
  },
  {
    label: 'Ingresos',
    icon: 'i-material-symbols-move-to-inbox-outline',
    to: 'entrances',
  },
  {
    label: 'Productos',
    icon: 'i-material-symbols-sell-outline',
    to: 'products',
  },
  {
    label: 'Usuarios',
    icon: 'i-material-symbols-group-outline-rounded',
    to: 'users',
  },
];

const sidebarBottomItems = [
  {
    label: 'Configuración',
    icon: 'i-material-symbols-settings-outline-rounded',
    to: 'settings',
  },
];
</script>
