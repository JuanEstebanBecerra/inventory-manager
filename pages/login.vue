<template>
  <div class="h-screen w-screen bg-gray-100 flex justify-center items-center">
    <div class="grid grid-cols-2 w-[1200px] h-[800px] shadow rounded-lg overflow-hidden">
      <div class="h-full w-full bg-white px-20 flex justify-center items-center">
        <div class="flex flex-col gap-8 w-full">
            <h1 class="text-3xl">Inventory Manager</h1>
          <UFormField label="Correo">
            <UInput
              icon="i-heroicons-user-20-solid"
              placeholder="Ingrese su correo"
              size="lg"
              class="w-full" />
          </UFormField>
          <UFormField label="Contraseña">
            <UInput
              icon="i-heroicons-key-20-solid"
              placeholder="********"
              type="password"
              size="lg"
              class="w-full" />
          </UFormField>
          <div class="h-8"></div>
          <UButton
            block
            label="Iniciar sesión"
            size="xl"
            to="/sells" />
        </div>
      </div>
      <div class="flex relative">
        <img
          class="absolute bottom-0 w-full h-full"
          src="assets/img/login.jpg" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts"></script>
