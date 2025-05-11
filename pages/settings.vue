<template>
  <div class="p-8 pt-4 flex flex-col gap-8 bg-gray-50 h-full">
    <div class="flex justify-between">
      <h1 class="text-3xl">Configuración</h1>
    </div>
    <div class="flex justify-center items-center">
      <div class="w-[1000px] h-[700px] bg-white shadow-md rounded-lg p-8">
        <span class="font-bold">Copia de seguridad</span>
        <div class="p-4 flex flex-col gap-4">
          <div class="flex justify-between gap-32 items-center">
            <div class="flex flex-col">
              <span class="font-semibold">Generar copia de seguridad</span>
              <p class="text-gray-500 text-sm">
                Esta funcionalidad permite crear una copia del estado actual de la base de datos. Es útil para
                resguardar la información de la aplicación y poder recuperarla en caso de pérdida, error o daño en los
                datos.
              </p>
            </div>

            <UButton
              variant="outline"
              color="neutral"
              icon="i-material-symbols-upload-file-outline-rounded"
              label="Generar copia de seguridad" />
          </div>

          <div class="flex justify-between gap-32 items-center">
            <div class="flex flex-col">
              <span class="font-semibold">Importar copia de seguridad</span>
              <p class="text-gray-500 text-sm">
                Esta funcionalidad permite restaurar la información de la aplicación a partir de un archivo de copia de
                seguridad previamente generado. Útil para recuperar datos luego de una pérdida.
              </p>
            </div>

            <UButton
              variant="outline"
              color="neutral"
              icon=i-material-symbols-sim-card-download-outline-rounded
              label="Importar copia de seguridad" />
          </div>
        </div>
      </div>
    </div>
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
  { id: 1, name: 'Arroz', provider: 'Bebidas del Valle', code: '751462', active: true, amount: 409, price: 3295 },
  { id: 2, name: 'Frijoles', provider: 'Bebidas del Valle', code: '737810', active: false, amount: 166, price: 2842 },
  { id: 3, name: 'Azúcar', provider: 'Aseo Hogar', code: '767997', active: false, amount: 22, price: 13438 },
  { id: 4, name: 'Aceite', provider: 'Comestibles Andinos', code: '139661', active: true, amount: 111, price: 8709 },
  { id: 5, name: 'Sal', provider: 'Alimentos del Sur', code: '960861', active: true, amount: 309, price: 10241 },
  {
    id: 6,
    name: 'Harina de Trigo',
    provider: 'Panadería San Juan',
    code: '946558',
    active: false,
    amount: 272,
    price: 7914,
  },
  { id: 7, name: 'Café', provider: 'Higiene Total', code: '902119', active: true, amount: 76, price: 1351 },
  {
    id: 8,
    name: 'Leche en Polvo',
    provider: 'Distribuciones Gourmet',
    code: '376770',
    active: false,
    amount: 107,
    price: 1455,
  },
  {
    id: 9,
    name: 'Pasta',
    provider: 'Distribuciones Gourmet',
    code: '105192',
    active: false,
    amount: 330,
    price: 14593,
  },
  { id: 10, name: 'Lentejas', provider: 'Granos del Norte', code: '897539', active: false, amount: 169, price: 10718 },
  { id: 11, name: 'Galletas', provider: 'Granos del Norte', code: '888957', active: true, amount: 93, price: 7929 },
  { id: 12, name: 'Atún', provider: 'Lácteos Nacionales', code: '846042', active: false, amount: 264, price: 6322 },
  { id: 13, name: 'Sardinas', provider: 'Lácteos Nacionales', code: '898527', active: true, amount: 289, price: 10518 },
  { id: 14, name: 'Maíz', provider: 'Productos del Campo', code: '121726', active: false, amount: 134, price: 7433 },
  { id: 15, name: 'Avena', provider: 'Productos del Campo', code: '345982', active: true, amount: 142, price: 11781 },
  {
    id: 16,
    name: 'Chocolate',
    provider: 'Distribuciones Gourmet',
    code: '324740',
    active: false,
    amount: 63,
    price: 14466,
  },
  { id: 17, name: 'Jabón', provider: 'Aseo Hogar', code: '641871', active: true, amount: 160, price: 9546 },
  {
    id: 18,
    name: 'Detergente',
    provider: 'Comestibles Andinos',
    code: '384251',
    active: false,
    amount: 166,
    price: 11290,
  },
  { id: 19, name: 'Shampoo', provider: 'Alimentos del Sur', code: '264203', active: false, amount: 349, price: 13236 },
  {
    id: 20,
    name: 'Cepillo de dientes',
    provider: 'Higiene Total',
    code: '109087',
    active: true,
    amount: 166,
    price: 6011,
  },
  {
    id: 21,
    name: 'Papel higiénico',
    provider: 'Lácteos Nacionales',
    code: '973703',
    active: false,
    amount: 41,
    price: 6806,
  },
  { id: 22, name: 'Toallas', provider: 'Aseo Hogar', code: '144875', active: true, amount: 64, price: 12577 },
  { id: 23, name: 'Desodorante', provider: 'Higiene Total', code: '770899', active: true, amount: 448, price: 5373 },
  {
    id: 24,
    name: 'Agua embotellada',
    provider: 'Comestibles Andinos',
    code: '645045',
    active: false,
    amount: 497,
    price: 6430,
  },
  { id: 25, name: 'Jugo', provider: 'Distribuciones Gourmet', code: '240537', active: true, amount: 27, price: 7639 },
  { id: 26, name: 'Refresco', provider: 'Granos del Norte', code: '327787', active: true, amount: 265, price: 6790 },
  { id: 27, name: 'Cerveza', provider: 'Productos del Campo', code: '935191', active: false, amount: 22, price: 13215 },
  { id: 28, name: 'Vino', provider: 'Distribuciones Gourmet', code: '802099', active: true, amount: 304, price: 6043 },
  { id: 29, name: 'Ron', provider: 'Aseo Hogar', code: '300313', active: true, amount: 85, price: 9111 },
  { id: 30, name: 'Whisky', provider: 'Panadería San Juan', code: '347808', active: true, amount: 78, price: 10265 },
  { id: 31, name: 'Pollo', provider: 'Higiene Total', code: '858598', active: true, amount: 408, price: 13716 },
  {
    id: 32,
    name: 'Carne',
    provider: 'Distribuciones Gourmet',
    code: '471247',
    active: false,
    amount: 202,
    price: 7310,
  },
  {
    id: 33,
    name: 'Pescado',
    provider: 'Distribuciones Gourmet',
    code: '133229',
    active: true,
    amount: 302,
    price: 11911,
  },
  { id: 34, name: 'Huevos', provider: 'Comestibles Andinos', code: '163230', active: false, amount: 85, price: 7771 },
  {
    id: 35,
    name: 'Mantequilla',
    provider: 'Granos del Norte',
    code: '256969',
    active: false,
    amount: 209,
    price: 6255,
  },
  {
    id: 36,
    name: 'Queso',
    provider: 'Distribuciones Gourmet',
    code: '586207',
    active: false,
    amount: 275,
    price: 9474,
  },
  {
    id: 37,
    name: 'Yogur',
    provider: 'Distribuciones Gourmet',
    code: '718146',
    active: false,
    amount: 483,
    price: 13297,
  },
  { id: 38, name: 'Pan', provider: 'Alimentos del Sur', code: '973746', active: true, amount: 130, price: 1422 },
  { id: 39, name: 'Gaseosa', provider: 'Productos del Campo', code: '236781', active: true, amount: 381, price: 11895 },
  { id: 40, name: 'Helado', provider: 'Comestibles Andinos', code: '231120', active: true, amount: 462, price: 7404 },
  {
    id: 41,
    name: 'Cereal',
    provider: 'Distribuciones Gourmet',
    code: '582541',
    active: false,
    amount: 448,
    price: 11131,
  },
  {
    id: 42,
    name: 'Sopa instantánea',
    provider: 'Panadería San Juan',
    code: '247052',
    active: false,
    amount: 317,
    price: 12348,
  },
  { id: 43, name: 'Salsa de tomate', provider: 'Aseo Hogar', code: '887514', active: true, amount: 199, price: 7980 },
  { id: 44, name: 'Mayonesa', provider: 'Alimentos del Sur', code: '828758', active: false, amount: 341, price: 13583 },
  { id: 45, name: 'Mostaza', provider: 'Panadería San Juan', code: '728452', active: true, amount: 316, price: 5815 },
  { id: 46, name: 'Vinagre', provider: 'Granos del Norte', code: '443999', active: false, amount: 238, price: 5941 },
  {
    id: 47,
    name: 'Mermelada',
    provider: 'Panadería San Juan',
    code: '976456',
    active: true,
    amount: 292,
    price: 10041,
  },
  { id: 48, name: 'Miel', provider: 'Distribuciones Gourmet', code: '213912', active: true, amount: 267, price: 6959 },
  { id: 49, name: 'Té', provider: 'Productos del Campo', code: '511061', active: true, amount: 55, price: 5922 },
  { id: 50, name: 'Yerba Mate', provider: 'Aseo Hogar', code: '178375', active: false, amount: 354, price: 8756 },
];
</script>
